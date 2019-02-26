---
description: >-
  This page describe how to setup taxes for your collectives to conform with
  local laws
---

# Taxes support \(VAT\)

{% hint style="warning" %}
This documentation is a work in progress, the feature is not available yet.
{% endhint %}

In certain countries or regions of the world, hosts are required to collect state taxes to conform with local legislation. Open Collective implements that in a flexible way to accomodate with most of the legilsations out there.

## Documentation

The configuration is made in the host `settings`, using the `tiersTaxes` key. This configuration must match the following schema:

```javascript
"tiersTaxes": {
	// Set the tier type on which the tax applies as the tax key
	// eg. SERVICE, PRODUCT, DONATION...
	"SERVICE": {
		// Tax name as displayed to the user
		"name": "VAT",
		// Description of the tax
		"description": "European valud-added tax",
		// An optionnal regex to validate tax identification numbers
		"identificationNumberRegex": "^((AT)?U[0-9]{8}|(BE)?0[0-9]{9}|(BG)?[0-9]{9,10}|(CY)?[0-9]{8}L(CZ)?[0-9]{8,10}|(DE)?[0-9]{9}|(DK)?[0-9]{8}|(EE)?[0-9]{9}(EL|GR)?[0-9]{9}|(ES)?[0-9A-Z][0-9]{7}[0-9A-Z]|(FI)?[0-9]{8}(FR)?[0-9A-Z]{2}[0-9]{9}|(GB)?([0-9]{9}([0-9]{3})?|[A-Z]{2}[0-9]{3})(HU)?[0-9]{8}|(IE)?[0-9]S[0-9]{5}L|(IT)?[0-9]{11}(LT)?([0-9]{9}|[0-9]{12})|(LU)?[0-9]{8}|(LV)?[0-9]{11}|(MT)?[0-9]{8}(NL)?[0-9]{9}B[0-9]{2}|(PL)?[0-9]{10}|(PT)?[0-9]{9}|(RO)?[0-9]{2,10}(SE)?[0-9]{12}|(SI)?[0-9]{8}|(SK)?[0-9]{10})$",
		// A list of countries where the tax applies. If omitted, tax will apply for all countries
		"countries": ["AT","BE","BG","HR","CY","CZ","DK","EE","FI","FR","DE","GR","HU","IE","IT","LV","LT","LU","MT","NL","PL","PT","RO","SK","SI","ES","SE","GB"],
		// Percentage of the tax
		"percentage": 20
	}
}
```

## Templates

### VAT \(Value Added Tax, Europe\)

```javascript
"tiersTaxes": {
	"PRODUCT": {
		"name": "VAT",
		"description": "European valud-added tax",
		"identificationNumberRegex": "^((AT)?U[0-9]{8}|(BE)?0[0-9]{9}|(BG)?[0-9]{9,10}|(CY)?[0-9]{8}L(CZ)?[0-9]{8,10}|(DE)?[0-9]{9}|(DK)?[0-9]{8}|(EE)?[0-9]{9}(EL|GR)?[0-9]{9}|(ES)?[0-9A-Z][0-9]{7}[0-9A-Z]|(FI)?[0-9]{8}(FR)?[0-9A-Z]{2}[0-9]{9}|(GB)?([0-9]{9}([0-9]{3})?|[A-Z]{2}[0-9]{3})(HU)?[0-9]{8}|(IE)?[0-9]S[0-9]{5}L|(IT)?[0-9]{11}(LT)?([0-9]{9}|[0-9]{12})|(LU)?[0-9]{8}|(LV)?[0-9]{11}|(MT)?[0-9]{8}(NL)?[0-9]{9}B[0-9]{2}|(PL)?[0-9]{10}|(PT)?[0-9]{9}|(RO)?[0-9]{2,10}(SE)?[0-9]{12}|(SI)?[0-9]{8}|(SK)?[0-9]{10})$",
		"countries": ["AT","BE","BG","HR","CY","CZ","DK","EE","FI","FR","DE","GR","HU","IE","IT","LV","LT","LU","MT","NL","PL","PT","RO","SK","SI","ES","SE","GB"],
		"percentage": 20
	}
}
```

