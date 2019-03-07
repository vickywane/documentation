---
description: Documenting how we handle translations in the code
---

# Translations

We use [react-intl](https://github.com/yahoo/react-intl) to manage our translations.

## FormattedMessage

The `FormattedMessage` component is the main way to translate strings. To use it, you just need to add the following import:

```javascript
import { FormattedMessage } from 'react-intl'
```

Then you just add the component with an unique `id` and a `defaultMessage`.

For VSCode users, you can use the following snippet to make your life easier:

```javascript
{
  "Formatted Message (react-intl)": {
    "scope": "javascript",
    "prefix": "formatted-message",
    "body": "<FormattedMessage id=\"$TM_FILENAME_BASE.$0\" defaultMessage=\"$1\"/>",
    "description": "Put the given string in a FormattedMessage"
  }
}

```

## Add a new language

To add translations for a new language, copy paste the `en.json` from `frontend/src/lang` and rename the copy using the 2 letter code for the country/language\).

You will also need to copy paste the last line in `frontend/scripts/translate.js`:

`fs.writeFileSync(LANG_DIR + 'ja.json', JSON.stringify(translatedMessages('ja'), null, 2));` and replace `ja` with your 2 letter locale code.

