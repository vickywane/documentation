---
description: Documenting how we handle translations in the code
---

# Internationalization \(i18n\) system

We use [react-intl](https://github.com/formatjs/react-intl) to manage our translations. They are extracted from the code to `src/lang/${locale}.json` files using the `npm run build:langs` command \(CI will notify you if the translation files are outdated\). **Don't translate the strings directly in the files**, we use [Crowdin](https://crowdin.com/project/opencollective) to manage our translatations.

## Good practices

### Use "select" when a value has a limited number of options

**Example**

```jsx
<FormattedMessage
    id="withSelect"
    defaultMessage="{action, select, delete {Delete this} archive {Archive this} other {Do something with this}}"
    values={{ action: 'delete' }}
/>

// => "Delete this"

<FormattedMessage
    id="withSelect"
    defaultMessage="{action, select, delete {Delete this} archive {Archive this} other {Do something with this}}"
    values={{ action: 'eat' }}
/>

// => "Do something with this"
```

* `defaultMessage` string breakdown:
  * `action` variable name
  * `select` keyword
  * `delete` and `archive` possible values
  * `other` all other values will use this key

**An exception to this rule:** very common enums or the ones with many possible values should be implemented as a separate file listing all values because:

* Re-usability
* A map of translations is easier to read than a long select string with tons of options

See [i18n-member-role](https://github.com/opencollective/opencollective-frontend/blob/6c164f4b683b5b7393242db537a95c0f033b1377/src/lib/i18n-member-role.js) as an example.

### Don't assume word's order stays the same in other languages

The order of the words may change from a language to another. For this reason we must always pass the values to be replaced in `values` so their order can later be changed.

**Example**

```jsx
// Bad
<div>
    <FormattedMessage id="str" defaultMessage="Pending approval from " />
    <Link route={`/${host.slug}`}>{host.name} </Link>
</div>

// Good
<div>
    <FormattedMessage 
        id="str" 
        defaultMessage="Pending approval from {host}" 
        values ={{ 
          host: <Link route={`/${host.slug}`}>{host.name} </Link>
        }}
    />
</div>
```

### Don't split strings

Splitting a string is alway problematic, because translators loose the context: the strings may not be next to each others when they'll be translated.

```jsx
// Bad
<FormattedMessage
  id="_"
  defaultMessage="Do you want to {createSomething} in this list?"
  values={{
    createSomething: (
      <blink>
        <FormattedMessage id="_" defaultMessage="create something"/>
      </blink>
    )
  }}
/>

// Good
<FormattedMessage
  id="_"
  defaultMessage="Do you want to <blink>create something</blink> in this list?"
  values={{
    createSomething: function BlinkComponent(msg) {
      return (<blink>{msg}</blink>)
    }
  }}
/>
```

### Use I18nFormatters to format rich text \(bold, italic...etc\)

```jsx
import I18nFormatters from '../../I18nFormatters';

<FormattedMessage 
  id="_" 
  defaultMessage="This <strong>is</strong> <i>easier</i>." 
  values={I18nFormatters}
/>
```

### Translate links inline

In some parts of the code we translate links like this:

```jsx
// Please don't do that!
<FormattedMessage
  id="ReadTheDocs"
  defaultMessage="Please check our {documentationLink} to learn more!"
  values={{
    documentationLink: (
      <a href="https://docs.opencollective.com">
        <FormattedMessage id="documentation" defaultMessage="documentation" />
      </a>
    ),
  }}
/>
```

This is bad because we're creating two strings and translators loose the context when they translate one. You should do this instead:

```jsx
import { getI18nLink } from './I18nFormatters';

// External link
<FormattedMessage
  id="ReadTheDocs"
  defaultMessage="Please check our <link>documentation</link> to learn more!"
  values={{
    link: getI18nLink({ href: 'https://docs.opencollective.com' }),
  }}
/>

// Internal link
import Link from './Link';

<FormattedMessage
  id="CheckHosts"
  defaultMessage="Please check <link>hosts page</link> to learn more!"
  values={{
    link: getI18nLink({ as: Link, route: 'hosts' }),
  }}
/>
```

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

#### Add the language on Crowdin

Just go to [https://crowdin.com/project/opencollective/settings\#translations](https://crowdin.com/project/opencollective/settings#translations), click on `Target languages` pick the language and click `Update`.

#### Activate the language in the code

To activate a language on the website, we usually wait to have a correct translated ratio \(20-30%\). Then activate it by adding a new line in [https://github.com/opencollective/opencollective-frontend/blob/master/lib/constants/locales.js](https://github.com/opencollective/opencollective-frontend/blob/master/lib/constants/locales.js).

