---
description: Describes what we expect from new code written for our product
---

# Best Practice Guidelines



* The strings must be internationalized. See [/help/developers/translations](https://docs.opencollective.com/help/developers/translations)
* Whenever it's possible we must use `styled-components` to write styles. See [OC Styleguide](https://opencollective-styleguide.now.sh/)
* We're getting rid of `Bootstrap`. Please don't use it for new developments.
* When adding new dependencies, we use [fixed versions](https://docs.npmjs.com/about-semantic-versioning).
* Icons must be imported from the [styled-icons](http://styled-icons.js.org/) library.
* Tests written with Cypress must follow our [good practices](https://docs.opencollective.com/help/developers/testing-with-cypress) conventions.
* Don't commit `package-lock.json` if you're not making any changes to the libraries.

## Special tips

* If the issue you're working on require changes in both API and Frontend, give your Git branches the same name. CI will automatically pull the correct API's branch when testing the frontend.

