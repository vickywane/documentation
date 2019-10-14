# Manual Reporting

To manually run the monthly report:

1- Update the template: [https://github.com/OpenCollective/opencollective-api/blob/master/templates/emails/group.monthlyreport.hbs](https://github.com/OpenCollective/opencollective-api/blob/master/templates/emails/group.monthlyreport.hbs)

2- If you want to preview some of the emails, you can run it locally with

```text
PG_DATABASE=opencollective_prod_snapshot DEBUG=preview npm run cron:monthly
```

\(it won't send real emails but it will output links to preview them in the browser\)

3- Run bash on heroku production:

```text
heroku run bash --app opencollective-prod-api
```

4- Run the monthly cron job manually:

```text
npm run cron:monthly
```

If you want to only run it for certain collectives, modify the `query` here: [https://github.com/OpenCollective/opencollective-api/blob/master/cron/monthly/email-report.js\#L30](https://github.com/OpenCollective/opencollective-api/blob/master/cron/monthly/email-report.js#L30)

