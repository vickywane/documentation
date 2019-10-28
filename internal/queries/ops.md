# Ops

## Detect duplicate orders

This will return the orders coming from the same and to collective and same amount within the same minute

```text
with res as (
  SELECT 
    substring(cast(DATE_TRUNC('minute', o."createdAt") as text) from 1 for 16) as minute,
    count(*) as count, "FromCollectiveId", "CollectiveId", "totalAmount", max(o."currency") as currency,
    o.description,
    MAX(s."isActive"::INT) as "activeSubscription"
  FROM "Orders" o
  LEFT JOIN "Subscriptions" s ON o."SubscriptionId"=s.id
  WHERE (s."isActive" IS TRUE OR s.id IS NULL) AND o."deletedAt" IS NULL AND o."processedAt" IS NOT NULL AND o."PaymentMethodId" IS NOT NULL
  GROUP BY "FromCollectiveId", "CollectiveId", "totalAmount", "minute", o."description"
  ORDER BY count DESC
)
SELECT fc.slug, fc.type, r.*
FROM res r
LEFT JOIN "Collectives" fc ON fc.id=r."FromCollectiveId"
WHERE count > 1 ORDER BY r.count DESC
```

