# Analytics

## Get annual budget and bunch of expenses stats per collective

### **WARNING: Don't run in production. Can take a while.**

```text
with "monthlySubscriptions" as
    (SELECT
      t."GroupId", COALESCE(SUM(t.amount * 12),0) as total
      FROM "Subscriptions" s
      LEFT JOIN "Donations" d ON s.id = d."SubscriptionId"
      LEFT JOIN "Transactions" t
      ON (s.id = d."SubscriptionId"
        AND t.id = (SELECT MAX(id) from "Transactions" t where t."DonationId" = d.id))
      WHERE t.amount > 0
        AND t."deletedAt" IS NULL
        AND s.interval = 'month'
        AND s."isActive" IS TRUE
        AND s."deletedAt" IS NULL
      GROUP BY t."GroupId"),

      "yearlyAndOneTimeSubscriptions" as
    (SELECT
      t."GroupId", COALESCE(SUM(t.amount),0) as total FROM "Transactions" t
      LEFT JOIN "Donations" d ON t."DonationId" = d.id
      LEFT JOIN "Subscriptions" s ON d."SubscriptionId" = s.id
      WHERE t.amount > 0
        AND t."deletedAt" IS NULL
        AND t."createdAt" > (current_date - INTERVAL '12 months') 
        AND ((s.interval = 'year' AND s."isActive" IS TRUE AND s."deletedAt" IS NULL) OR s.interval IS NULL)
      GROUP BY t."GroupId"),

    "inActiveSubscriptions" as
    (SELECT
      t."GroupId", COALESCE(SUM(t.amount),0) as total FROM "Transactions" t
      LEFT JOIN "Donations" d on t."DonationId" = d.id
      LEFT JOIN "Subscriptions" s ON d."SubscriptionId" = s.id
      WHERE t.amount > 0
        AND t."deletedAt" IS NULL
        AND t."createdAt" > (current_date - INTERVAL '12 months')
        AND s.interval = 'month' AND s."isActive" IS FALSE AND s."deletedAt" IS NULL
      GROUP BY t."GroupId"),

    "expensesData" as 
        (select e."GroupId", e.status, count(*) as "countExpenses", sum(amount) as "totalExpenses", max("createdAt") as "lastExpenseDate" from "Expenses" e
        WHERE "deletedAt" is null
        GROUP BY "GroupId", status
        ORDER BY "GroupId")

SELECT 
    id as "groupId", 
    slug, 
    COALESCE(ms.total,0)/100 + COALESCE(ys.total,0)/100 + COALESCE(ias.total,0)/100 as "annualBudget",
    currency, 
    ed.status as "expenseStatus",
    ed."lastExpenseDate",
    ed."countExpenses", 
    ed."totalExpenses"/100 as "sumOfExpenses"

     from "Groups" g
LEFT JOIN "monthlySubscriptions" ms on ms."GroupId" = g.id
LEFT JOIN "yearlyAndOneTimeSubscriptions" ys on ys."GroupId" = g.id
LEFT JOIN "inActiveSubscriptions" ias on ias."GroupId" = g.id
LEFT JOIN "expensesData" ed on ed."GroupId" = g.id
ORDER BY g.id
```

## Get backercount and core contributors

```text
with "backers" as 
(select "GroupId", count(*) as "backerCount" from "UserGroups"
    where role = 'BACKER'
    GROUP BY "GroupId")

select 
    g.id as "groupId", 
    g.name as "groupName",
    g.slug as "groupSlug",
    u.id as "userId",
    u."firstName" as "userFirstName", 
    u."lastName" as "userLastName", 
    u.email as "userEmail", 
    u.username as "username", 
    u.website as "userWebsite",
    u."twitterHandle" as "userTwitter",
    ug.role,
    b."backerCount"
from "UserGroups" ug
LEFT JOIN "Groups" g on ug."GroupId" = g.id
LEFT JOIN "Users" u on ug."UserId" = u.id
LEFT JOIN "backers" b on ug."GroupId" = b."GroupId"
WHERE ug.role = 'MEMBER' OR ug.role = 'HOST'
ORDER BY g.id
```

### Count of how many orders have updated paymentMethod after a failed charge

```text
with subs as 
(select distinct(id) as id, max("chargeRetryCount") as "chargeRetryCount" from "SubscriptionHistories" sh where "deletedAt" is null and "chargeRetryCount" > 0 group by id)

select oh.id, max("FromCollectiveId") as "FromCollectiveId", max("SubscriptionId"), max("chargeRetryCount") as "subId" 
from "OrderHistories" oh 
left join subs s on oh."SubscriptionId" = s.id
where "chargeRetryCount" > 0
group by oh.id having count("PaymentMethodId") > 1
```

