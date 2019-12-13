---
description: Describe the moderation system works and how the team should use it
---

# Internal moderation tools

{% hint style="warning" %}
We don't provide any interface for the moderation features yet. To access them you'll need a direct access to the database - through Forest, PgAdmin, DBeaver...etc
{% endhint %}

### Limit user account

#### What

* All features \(submitting expenses, commenting...\) will be blocked for this user.
* A warning will be displayed at the top of all pages for this user.

![](../.gitbook/assets/image%20%287%29.png)

#### When

User is clearly spamming or trying malicious things on the platform.

#### How

Set `User.data.features.ALL` to `false`

### Limit specific feature

#### What

The specified feature will be blocked for this user.

#### When

User has a strange behavior with a feature. We want to prevent the use of it without blocking access to the others.

#### How

Set `User.data.features.{FEATURE_NAME}` to `false`

To see a list of all features names, check [https://github.com/opencollective/opencollective-api/blob/master/server/constants/features.ts](https://github.com/opencollective/opencollective-api/blob/master/server/constants/features.ts)

**Example**

* Disable access to expenses: `User.data.features.EXPENSES = false` 
* Disable access to conversations: `User.data.features.CONVERSATIONS = false` 

