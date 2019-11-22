# Integrations

## Zapier Integration

We now provide a Zapier App! Zapier should be the default choice whenever you need to integrate Open Collective with a third party service. All you need is:

* To create an API key on [http://opencollective.com/applications](http://opencollective.com/applications)
* To add the app on [https://zapier.com/developer/public-invite/21484/63399c65bb01d75e00fe091ae7f58683/](https://zapier.com/developer/public-invite/21484/63399c65bb01d75e00fe091ae7f58683/)

Like everything we do, our Zapier app is open source \(MIT\). If you need an action that's not yet on the Zapier app and feel ready to work on the integration: check [https://github.com/opencollective/opencollective-zapier/settings](https://github.com/opencollective/opencollective-zapier/settings)

Otherwise feel free to open an issue on [https://github.com/opencollective/opencollective/issues](https://github.com/opencollective/opencollective/issues) to ask for it. Please tell us about our use case, we love to understand why our users do what they do!

## Twitter Integration

Connect your Twitter to automatically thank new backers who contribute to your Collective! To do so, go to your Collective page, click on the gear icon and head to the **Connected Accounts** page.

![](../.gitbook/assets/collectives_integrations_connected-accounts.png)

![](../.gitbook/assets/connect-twitter.png)

## Chat Integrations

You can set up Open Collective notifications in your Slack or Gitter channel. First set up a webhook, described below, and then [send it to us](mailto:ops@opencollective.com?subject=slack%20integration) and we'll add the hook to our platform.

### Slack Webhook

* In Slack, select menu **Apps & Integrations**
* Click **Build Your Own** &gt; **Make a Custom Integration** &gt; **Incoming WebHooks**
* Choose a channel, or create a new channel, where the notifications will be sent
* Click on **Add Incoming WebHooks Integration**

### **Gitter Webhook**

* Go to your room's integrations and click **Open Collective**
* Copy the provided Webhook URL and click **Done**

### For Admins

The webhook can be added in the database `Notifications` table:

```text
INSERT INTO "Notifications" (
  "GroupId",
  channel,
  type,
  active,
  "webhookUrl")
VALUES ((SELECT id from "Groups" where slug = '<group slug>'),
        '<channel: either slack or gitter',
        '<type: see note below>',
        true,
        '<webhook URL>');
```

`type` \(would actually be more properly named `activity`\) can be:

* either `'all'` \(\*\) to send notifications for all activities \(group transaction created, payment received from Stripe, etc\)
* or some constant from [here](https://github.com/OpenCollective/opencollective-api/blob/master/server/constants/activities.js) to only send notifications for a specific activity

[Some activities](https://github.com/OpenCollective/opencollective-api/blob/master/server/constants/activities.js#L6) are not linked to any group and will therefore be ignored.

