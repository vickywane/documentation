# Custom Strings

There are plenty of strings throughout the app that you may want to customize. This page will guide you to where you can go and edit them in the code. Don't forget to submit your change as a pull request!

### Localization

We use a very simple `strings.json` file for all the strings. We currently support English, Spanish and French. [https://github.com/OpenCollective/opencollective-website/blob/master/frontend/src/ui/strings.json](https://github.com/OpenCollective/opencollective-website/blob/master/frontend/src/ui/strings.json)

To add a translation to a new language, copy paste the [en.json](https://github.com/opencollective/frontend/blob/master/src/lang/en.json) from [frontend/src/lang](https://github.com/opencollective/frontend/tree/master/src/lang) and rename the filename using the 2 or 4 letter code for your country/language \(e.g. `fr-BE.json` or `fr.json`\).

You will also need to copy paste the last line in [frontend/scripts/translate.js](https://github.com/opencollective/frontend/blob/master/scripts/translate.js#L47)

```text
fs.writeFileSync(LANG_DIR + 'ja.json', JSON.stringify(translatedMessages('ja'), null, 2));
```

and replace `ja` with your 2-4 letter locale code.

Then you can submit a pull request, like this one :-\) [https://github.com/opencollective/frontend/pull/119](https://github.com/opencollective/frontend/pull/119)

### Custom email receipts & notifications

[https://github.com/OpenCollective/opencollective-api/tree/master/templates/emails](https://github.com/OpenCollective/opencollective-api/tree/master/templates/emails)

