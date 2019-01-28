# Custom Tweets

### Manual config for thank you Tweets

Instead of the [default thank you Tweets](../collectives/integrations.md#twitter-integration), it can be set up manually in `Group.settings` JSON object in database:

```text
{
  // thank you message immediately when receiving donation
  thankDonationEnabled: true,
  thankDonation: '$backer thanks for backing us!',

  // thank you message to all backers on 1st day of the month
  monthlyThankDonationsEnabled: true,
  monthlyThankDonationsSingular: 'Thank you $backer for supporting our collective',
  monthlyThankDonationsPlural: 'Thanks to our $backerCount backers and sponsors $backerList for supporting our collective'
}
```

 

