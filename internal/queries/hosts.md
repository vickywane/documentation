# Hosts

## Revenue

Revenue per month \(host fees\)

```text
SELECT 
  substring(cast(DATE_TRUNC('month', t."createdAt") as text) from 1 for 7) as month,
  -SUM("hostFeeInHostCurrency") / 100 as revenue FROM "Transactions" t
WHERE t."HostCollectiveId"=11004
  AND t.currency='USD'
  AND t."deletedAt" is null
  AND t.type = 'CREDIT'
GROUP BY month
ORDER BY month DESC
```

## Backers

Top backers within a certain time frame. Example with the host "Open Source Collective 501c6" \(id: 11004\) for 2018:

```text
SELECT
  CONCAT('https://opencollective.com/', max(c.slug)) as "backer",
  SUM(amount) / 100 as "amount",
  max(t.currency) as "currency"
FROM "Transactions" t
LEFT JOIN "Collectives" c ON c.id=t."FromCollectiveId"
WHERE t.type='CREDIT'
  AND (t."HostCollectiveId"=11004)
  AND t."deletedAt" IS NULL
  AND t."createdAt" >= '2018-01-01'
  AND t."createdAt" < '2019-01-01'
GROUP BY t.currency, t."FromCollectiveId"
ORDER BY amount DESC
```

## Expenses

Get all the pending and approved expenses \(not PAID\) from all the collectives \(example with the Open Source Collective Host \(id 772\)\)

For each expense, we show the balance available in the collective. Note that the amount of the expense does not include the payment processor fees \(so an expense of $100 cannot be paid via PayPal if the balance of the collective is $100\). Fees are usually 2.9% + $0.30 but could be higher for international payments.

```text
WITH 
  collectives AS (
    SELECT c.id, c.slug, m."MemberCollectiveId" FROM "Collectives" c
    LEFT JOIN "Members" m ON m."CollectiveId"=c.id
    WHERE m."MemberCollectiveId"=9805 OR m."MemberCollectiveId" = 8674 or m."MemberCollectiveId" = 9807
  ),
  balances AS (
    SELECT "CollectiveId", sum("netAmountInCollectiveCurrency") / 100 as balance
    FROM "Transactions"
    WHERE "deletedAt" IS NULL
    GROUP BY "CollectiveId"
  )
SELECT 
  e."createdAt",
  c."MemberCollectiveId" as hostId, 
  CONCAT('https://opencollective.com/',c.slug,'/expenses') as collective,
  b.balance, e.description, e.amount / 100 as amount, e.currency,
  e.category, e.status, e.attachment, e."payoutMethod", e."privateMessage"
FROM "Expenses" e 
INNER JOIN collectives c ON c.id=e."CollectiveId"
LEFT JOIN "Users" u ON u.id=e."UserId"
LEFT JOIN balances b ON b."CollectiveId" = e."CollectiveId"
WHERE e.status IN ('PENDING', 'APPROVED') AND e."deletedAt" IS NULL
```

### Get the breakdown of host fees per collective

```text
SELECT MAX(c.slug) as collective, SUM("hostFeeInHostCurrency") as "totalHostFeesInCents"
FROM "Transactions" t LEFT JOIN "Collectives" c ON c.id=t."CollectiveId"
WHERE t.type='CREDIT' AND c."HostCollectiveId" = 9802 AND t."createdAt" < '2018-01-01'
GROUP BY c.slug ORDER by "totalHostFeesInCents" DESC
```

### US taxes: 1099

Get all people to whom a host paid more than $600 in a given year in given categories. And get all the expenses from those people.

```text
WITH "totalExpenses" AS (
  SELECT "UserId", (SUM(amount) / 100) as "totalAmount"
  FROM "Expenses" e
  WHERE e."createdAt" >= '2016-01-01' AND e."createdAt" < '2017-01-01'
  AND e.currency = 'USD'
  AND e.status = 'PAID'
  GROUP BY "UserId"
 )

SELECT g.slug, u.username, u."firstName", u."lastName", u."email", e.title, e.category, (e.amount/100) as amount, e.currency, e.attachment
FROM "Expenses" e 
LEFT JOIN "totalExpenses" te ON te."UserId" = e."UserId"
LEFT JOIN "Users" u ON u.id = e."UserId"
LEFT JOIN "Groups" g on g.id = e."GroupId"
WHERE te."totalAmount" >= 600 
AND g.slug NOT LIKE '%wwcode%'
AND e."deletedAt" is NULL
AND e.category IN ('Office', 'Engineering', 'Other')
AND u.username NOT IN ('xdamman', 'piamancini')
ORDER BY u.id
```

### Hosts and collectives with currency mismatch

```text
SELECT
  count(*) as count, max(hc.slug) as "host", max(hc.id) as "HostCollectiveId",
  max(hc.currency) as "host.currency",
  max(c.slug) as "collective", max(c.currency) as "collective.currency",
  max(t.currency) as "transaction.currency",
  max(t."hostCurrency") as "transaction.hostCurrency",
  upper(t.data -> 'balanceTransaction' ->> 'currency') as "stripe.currency",
  min(t."createdAt") as "firstTransactionAt",
  max(t."createdAt") as "lastTransactionAt"
FROM "Transactions" t
LEFT JOIN "Collectives" hc ON hc.id=t."HostCollectiveId"
LEFT JOIN "Collectives" c ON c.id=t."CollectiveId"
WHERE t."hostCurrency" != hc.currency
  AND t."deletedAt" IS NULL
GROUP BY t."HostCollectiveId", t."CollectiveId", "stripe.currency"
ORDER BY count DESC
```

