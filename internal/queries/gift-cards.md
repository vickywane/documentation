# Gift Cards

## Gift cards created and claims per month

```text
SELECT 
date_trunc('month', pm."createdAt") as "month",
count(*),
sum(
CASE
WHEN pm."CollectiveId" = spm."CollectiveId" THEN 0
WHEN pm."CollectiveId" != spm."CollectiveId" THEN 1
END) as "totalClaimed"
FROM "PaymentMethods" pm
LEFT JOIN "PaymentMethods" spm ON spm.id=pm."SourcePaymentMethodId"
WHERE pm.service='opencollective'
  AND pm.type='virtualcard'
GROUP by month
```

## Total amount donated using gift cards by issuer and currency

```text
SELECT max(spmc.slug) as "gift card issuer", sum(amount) / 100 as "totalAmount", t.currency
FROM "Transactions" t
LEFT JOIN "PaymentMethods" pm ON t."PaymentMethodId" = pm.id
LEFT JOIN "PaymentMethods" spm ON pm."SourcePaymentMethodId" = spm.id
LEFT JOIN "Collectives" spmc ON spmc.id = spm."CollectiveId"
WHERE t.type = 'CREDIT'
  AND t."OrderId" IS NOT NULL
  AND pm.service = 'opencollective'
  AND pm.type = 'virtualcard'
GROUP BY spm."CollectiveId", t.currency
```

## Total number of Github contributors reached

This query will show a company how many unique contributors are participating to projects they have donated to through gift cards. Useful for companies that are donating to open-source as a way to promote their services to developers.

```sql
SELECT count(*) FROM (
    SELECT * FROM (
        SELECT json_object_keys((c.DATA ->> 'githubContributors')::json) AS contributors
        FROM "Transactions" t
        INNER JOIN "Collectives" c ON c.id = t."CollectiveId"
        WHERE t."UsingVirtualCardFromCollectiveId" = -- PUT THE COLLECTIVE ID HERE --
        AND t."type" = 'CREDIT'
        AND c.DATA IS NOT NULL
        AND c.DATA ->> 'githubContributors' IS NOT null
        GROUP BY c.id
    ) AS all_contributors
    GROUP BY contributors
) AS total_contributors
```

