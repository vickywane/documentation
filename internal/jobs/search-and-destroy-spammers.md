---
description: Monthly job to search and ban spammers from the platform
---

# Search & destroy spammers

## Job Info

{% hint style="info" %}
**Assignee**: Benjamin Piouffle  
**Frequency**: Monthly
{% endhint %}

## Procedure

### Search for spammers

* Go to [https://opencollective.com/search ](https://opencollective.com/search)
* Or use a query like the following one:

```sql
SELECT * FROM "Collectives"
WHERE  slug LIKE '%keto%'  -- replate by searched keywords
OR     website LIKE '%keto%'
OR     description LIKE '%keto%'
OR     "longDescription" LIKE '%keto%'
```

Out of the current research, the keywords that are interesting to look for are:

```text
keto, pills, sex, drug, porn, casino, webcam
```

### Ban spammers

Refer to [this page](../moderation.md#ban-users-and-collectives-permanently) for more info about banning users and collectives.

