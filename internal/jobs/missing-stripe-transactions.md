---
description: Monthly job to search and re-conciliate missing Stripe transactions
---

# Missing stripe transactions

## Job Info

{% hint style="info" %}
**Assignee**: Benjamin Piouffle  
**Frequency**: Monthly
{% endhint %}

## Procedure

```sql
-- Get the stripe username for the OSC host
SELECT username 
FROM "ConnectedAccounts" c 
WHERE "CollectiveId" = 11004 
AND service = 'stripe'
```

```bash
# Go to the API repository
cd opencollective-api

# Connect to heroku
heroku run bash --app opencollective-prod-api

# Run diff script. 1000 is the number of items to fetch
npm run script scripts/diff-stripe-transactions.js acct_xxxxxxxx 1000

# You can also add a transaction ID to start fetching from that transaction
npm run script scripts/diff-stripe-transactions.js acct_xxxxxxxx 1000 ch_xxxxx
```

## Job logs

All missing transactions should be added to [https://docs.google.com/spreadsheets/d/17t2AmUxyZN9U6SMN75AoHGGQ6r7rwqsOXPlOM8CJ0vc/edit\#gid=0](https://docs.google.com/spreadsheets/d/17t2AmUxyZN9U6SMN75AoHGGQ6r7rwqsOXPlOM8CJ0vc/edit#gid=0). The "Audit" tab should be updated to log today's date when running the job.

