# Gift Cards

### Gift cards created and claims per month

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

###  

### Total amount donated using gift cards by issuer and currency

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

