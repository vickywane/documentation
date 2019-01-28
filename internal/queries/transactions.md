# Transactions

This exports transactions with the slug of the collective, the host, the backer, the payment method used and all the associated fees.

```text
SELECT 
  t."createdAt", c.slug as "collective slug", t.type as "transaction type", t.amount, t.currency,
  fc.slug as "from slug", fc.type as "from type", t.description, e.category as "expense category", h.slug as "host slug",
  t."hostCurrency", t."hostCurrencyFxRate", 
  pm.service as "payment processor", pm.type as "payment method type",
  t."paymentProcessorFeeInHostCurrency", t."hostFeeInHostCurrency", t."platformFeeInHostCurrency"
FROM "Transactions" t
LEFT JOIN "Collectives" fc ON fc.id=t."FromCollectiveId"
LEFT JOIN "Collectives" c ON c.id=t."CollectiveId"
LEFT JOIN "Collectives" h ON h.id=t."HostCollectiveId"
LEFT JOIN "PaymentMethods" pm ON pm.id=t."PaymentMethodId"
LEFT JOIN "Expenses" e ON e.id=t."ExpenseId"
WHERE t."createdAt" >= '2018-08-01' AND t."createdAt" < '2018-11-01'
  AND t."deletedAt" IS NULL
ORDER BY t.id ASC
```

