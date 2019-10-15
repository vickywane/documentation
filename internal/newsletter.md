# Newsletter

We send a newsletter once a month to our wider community of users and supporters. This is done via Mailchimp. 

## Newsletter Process

### Signups

People can subscribe to the newsletter using the form at the bottom of the homepage.

### Import Recipients

Users who create new platform accounts and opt-in to the newsletter need to be added manually. A developer with database access needs to export the data. Then use Mailchimp's 'import contacts' function to add them to the main mailing list.

### Content

Content can come from a range of sources. 

Examples:

* Announcing new features or improvements
* Tweets about Open Collective or a specific Collective
* Blog posts by Open Collective
* Blog posts and articles by other people
* Media like podcasts or videos of talks
* Exciting partnerships with sponsors
* Tips and ideas for Collective fundraising
* New noteworthy Collectives that joined

The general style is brief and straightforward, with opportunities to click through for more info.

### Leaderboard

The monthly leaderboard is a popular section of the newsletter, showing top backers & sponsors, top Collectives by new backers, and top new Collectives by donations. To get this data, use the following queries, and then put the data in the team Google Drive.

#### Top backers

```sql
with res as (SELECT CONCAT('https://opencollective.com/', max(backer.slug)) as backer, sum(amount) / 100 as "amount", max(t.currency) as currency, string_agg(DISTINCT c.slug, ', ') AS "collectives supported", max(backer."twitterHandle") as twitter, max(backer.description) as description, max(backer.website) as website
FROM "Transactions" t
LEFT JOIN "Collectives" backer ON backer.id = t."FromCollectiveId"
LEFT JOIN "Collectives" c ON c.id = t."CollectiveId"
WHERE t."createdAt" > '2019-01-01'
  AND t."createdAt" < '2019-02-01'
  AND t.type='CREDIT'
  AND t."platformFeeInHostCurrency" < 0
  AND t."deletedAt" IS NULL
 GROUP BY t."FromCollectiveId"
 ORDER BY "amount" DESC)
 SELECT row_number() over(order by "amount" DESC) as "#", * from res
```

#### Top collectives by number of new backers

```sql
SELECT max(c.slug) as collective, max(c."createdAt") as "createdAt", count(*) as "totalNewBackers", max(c.website) as website, max(c."twitterHandle") as twitter, max(c.description) as description
FROM "Members" m
LEFT JOIN "Collectives" c ON m."CollectiveId" = c.id
WHERE m."createdAt" > '2019-01-01'
  AND m."createdAt" < '2019-02-01'
  AND m.role='BACKER'
GROUP BY "CollectiveId"
ORDER BY "totalNewBackers" DESC
```

#### Top new collectives by amount received

```sql
SELECT sum(amount) / 100 as "totalAmount", max(t.currency) as currency, max(c.slug) as collective, max(c.website) as website, max(c."twitterHandle") as twitter, max(c.description) as description
FROM "Transactions" t
LEFT JOIN "Collectives" c ON c.id = t."CollectiveId"
WHERE t."createdAt" > '2019-01-01'
  AND c."createdAt" > '2019-01-01'
  AND t."createdAt" < '2019-02-01'
  AND c."createdAt" < '2019-02-01'
  AND t.type='CREDIT'
  AND t."platformFeeInHostCurrency" < 0
 GROUP BY t."CollectiveId"
 ORDER BY "totalAmount" DESC
```

#### List of transactions

```sql
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
WHERE t."createdAt" >= '2019-01-01' AND t."createdAt" < '2019-02-01'
  AND t."deletedAt" IS NULL
ORDER BY t.id ASC
```



