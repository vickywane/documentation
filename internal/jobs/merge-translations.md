---
description: A weekly job to merge translations from Crowdin
---

# Merge translations

## Job Info

{% hint style="info" %}
**Assignee**: Benjamin Piouffle  
**Frequency**: Weekly
{% endhint %}

## Procedure

Crowdin opens a branch at `i18n/crowdin` . It's good to merge this branch at least once a week. The process to follow is this one:

1. Go to [https://crowdin.com/project/opencollective/settings\#integration](https://crowdin.com/project/opencollective/settings#integration) and click on `Sync now` to force synchronization.
2. Go to the frontend repo. Wait for the synchronization to be done, then pull the `i18n/crowdin` branch.
3. Merge master **into** `i18n/crowdin`, push result. **In case of conflicts, always take the version from `i18n/crowdin`**.
4. Push the result, wait for CI to pass.
5. **SQUASH** and merge the changes. Don't forget to **Squash**! This is really important, Crowdin sometimes pushes hundreds of commits, we don't want to overload the history.



