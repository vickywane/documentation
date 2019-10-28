# Collectives

## Stats

### Top backers

```text
SELECT max(c.name) as backer, concat('https://opencollective.com/',max(c.slug)) as "backer profile", 
  sum(t."amount")/ 100 as "totalAmount", max(t.currency) as currency
FROM "Transactions" t
LEFT JOIN "Collectives" c ON c.id = t."FromCollectiveId"
WHERE t."CollectiveId"=19965
  AND t.type='CREDIT'
  AND t."deletedAt" IS NULL
GROUP BY t."FromCollectiveId"
ORDER BY "totalAmount" DESC
```

### Revenue breakdown per tier

```text
SELECT max(t.name) as ticket, sum(o.quantity) as count,
  sum("totalAmount") / 100 as "totalAmount", max(o.currency) as currency
FROM "Orders" o
LEFT JOIN "Tiers" t ON t.id = o."TierId"
WHERE o."CollectiveId"=19965
  AND o.status='PAID'
  AND o."deletedAt" IS NULL
GROUP BY o."TierId"
```

### Breakdown of expenses

```text
WITH expenses AS (
  SELECT max(category) as category, max(description) as description,
    sum(amount) as amount, max(currency) as currency
  FROM "Expenses"
  WHERE "CollectiveId"=19965
  GROUP BY description
  ORDER BY amount DESC
)
SELECT max(category) as category, count(*) as count,
  sum(amount) / 100 as "totalAmount", max(e.currency) as currency,
  string_agg(concat(e.description, ' (', e.currency, ' ',e.amount / 100,')'), ', ') as "expenses"
FROM "expenses" e 
GROUP BY category
ORDER BY "totalAmount" DESC
```

List of backers with first and last donation

```text
SELECT o."createdAt", MAX(s."updatedAt") as "updateAt", bool_and(s."isActive") as "isActive", MAX(t."createdAt") as "lastTransactionAt", MAX(backer.slug) as "profile", o."totalAmount" as "orderAmount", SUM(t.amount) as "totalAmountInCents"
FROM "Orders" o
LEFT JOIN "Subscriptions" s ON s.id = o."SubscriptionId"
LEFT JOIN "Collectives" c on c.id = o."CollectiveId"
LEFT JOIN "Collectives" "backer" on backer.id = o."FromCollectiveId"
LEFT JOIN "Transactions" t ON t."OrderId" = o.id
WHERE c.slug='babel' AND t.type='CREDIT'
GROUP BY o.id
ORDER BY "totalAmountInCents" DESC
```

Number of donations and total donations per month per collective

```text
SELECT 
  substring(cast(DATE_TRUNC('month', t."createdAt") as text) from 1 for 7) as month,
  MAX(g.slug) as collective,
  count(t.*) as "totalDonations", 
  SUM(t.amount)/100 as "totalDonationsAmount",
  (SUM(t.amount)/100)/count(t.*) as "avgDonation",
  MAX(g.currency) as "currency"

FROM "Transactions" t LEFT JOIN "Collectives" g ON t."CollectiveId" = g.id 
WHERE t.type='CREDIT' AND t."deletedAt" is NULL AND slug = 'webpack' AND t."PaymentMethodId" IS NOT NULL
GROUP BY month
ORDER BY month ASC
```

## Export

### Export all backers of a collective with private data \(user.email\)

```text
SELECT mc."createdAt", m.role, u.email, mc.name, mc.description, mc.website, mc."twitterHandle"
FROM "Collectives" c
  LEFT JOIN "Members" m ON m."CollectiveId" = c.id 
  LEFT JOIN "Collectives" mc ON m."MemberCollectiveId" = mc.id 
  LEFT JOIN "Users" u ON u."CollectiveId" = mc.id 
WHERE c.slug='becoworking' AND m.role != 'HOST'
```

### New collectives for the past XX and creator details

```text
select 
    c.id as "collectiveId", 
    slug, 
    c."createdAt" as "collectiveCreatedAt", 
    "HostCollectiveId", 
    tags,
    u."firstName" as firstname,
    u."lastName" as lastname,
    u.email as email
from "Collectives" as c
left join "Users" u on c."CreatedByUserId" = u.id
where 
    type ilike 'collective' 
    and c."deletedAt" is null
    and u."deletedAt" is null 
    and c."createdAt" > '2017-11-15';
```

### Expenses

Note: this export includes private data \(user.email, expense.attachment\)

```text
SELECT 
  e."incurredAt", 
  e.status, 
  e.amount, 
  e.currency, 
  e.category, 
  e.description, 
  e."privateMessage", 
  e.attachment,
  u."firstName", 
  u."lastName", 
  u.email
FROM "Expenses" e 
LEFT JOIN "Users" u on e."UserId" = u.id
WHERE e."CollectiveId" = 302
```

## Administration

### Cancel all active subscriptions

Need to update `CollectiveId` \(here 967\) and `deactivatedAt`

```text
BEGIN;

with subscriptions as (
  SELECT "SubscriptionId" as id
  FROM "Orders"
  WHERE "CollectiveId"=967 AND status='ACTIVE'
)
UPDATE "Subscriptions"
SET "isActive" = false, "deactivatedAt" = '2018-10-27'
WHERE id IN (select id from "subscriptions");

UPDATE "Orders" SET status = 'CANCELLED'
WHERE status='ACTIVE' AND "CollectiveId" = 967;

COMMIT;
```

