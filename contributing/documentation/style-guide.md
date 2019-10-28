---
description: A reference for writing style and formatting
---

# Style guide

This is a reference guide to our documentarians. It wasn't created to limit you; instead, it should help you understand the overall style of our documentation and teach you how to reproduce it!

## Language and writing style

* Use inclusive language.
* Write as you were having a chat with our readers. Address them directly.
* Keep it simple and short: avoid jargons, long sentences and uncommon words.
* When in doubt, use US English as a reference for spelling.
* For headings, buttons, menu items and page names, use sentence case \(as in _Suggesting changes_\). Title case \(as in _Fiscal Host_\) should be used only when referring to features or specific roles.

### Contractions

You are encouraged to use contractions as long as it doesn't make sentences difficult to read.

| Use | Avoid |
| :--- | :--- |
| It's \(as in 'it is'\), can't, wouldn't, you're, you've, don't or do not | It is, cannot, would not, it'll, it's \(as in 'it has'\) |

### **Capitalization**

**Always** capitalize the following terms:

* Collective
* Organization
* Fiscal Host
* Admin \(Collective Admin, Fiscal Host Admin\)
* Core Contributor

When referring specifically to the feature on our platform, **always** capitalize:

* Update
* Event
* Expense
* Transaction

**Do not capitalize** the above words when they do not refer to the name of a role or entity on the platform. For example:

> You can think of Fiscal Hosts as umbrella organizations for Collectives.

**Fiscal Hosts** and **Collectives** are capitalized because they refer to names of roles on the platform, but **organization** is not because it's used here as part of the common phrase **umbrella organization**.

### **Words to avoid**

There are a lot of names and terms we have used in the past or that have common meanings close to roles and entities on the platform. It's important to use language that your intended audience will understand and identify with, so no words are banned, but be mindful of using the below terms as they can easily introduce confusion.

#### **User**

Everyone is a user, so it's not super helpful when trying to refer to something more specific.

#### **Sponsor**

This is a common word to describe when a company gives money to a project, but it \_\*\*\_has caused confusion because sometimes sponsorship is defined by the kind of entity making the financial contribution \(company vs individual\), and sometimes it's defined by how much they are contributing \(e.g. some Collectives call everything over $1000 'sponsorship' regardless of who gives it\). Collectives can each define these things for themselves, so it's safer to refer to "individual financial contributor" or "organizational financial contributor".

#### **Backer**

Similar to the above. If a company gives only $5 a month, are they a backer or a sponsor? That's undefined globally, so stick with "financial contributor".

#### **Donate, back, support, join, or any other synonym for financial contribution**

Because different Collectives use different terms, the platform should not try to decide for them. Each community will have its own context. Therefore we have decided to stick with the words "contribute" and "contribution" and add the qualifier "financial" when it's through money.

#### **Subscription**

We used to call recurring financial contributions "subscriptions", but this proved problematic because most Collectives don't think of someone giving $5 a month as "subscribing" to them, and it's also easy to confuse with the concept of subscribing to Updates and getting emails. To emphasize our key action of "contribution" we call it "recurring financial contributions". We are aware this is too long, but we haven't come up with a better idea so far.

#### **Chapter**

Previously, we explored the idea of calling Open Collective branded fiscal hosts \(Open Collective Europe, Open Collective UK, etc\) "chapters". But this concept was not followed up and supported and using the word is confusing. These are simply Fiscal Hosts.

## Formatting

Write in Markdown. To know more GitBook's implementation of Markdown, check [their reference guide](https://docs.gitbook.com/content-editing/markdown).

{% hint style="warning" %}
Remember to use `\` any time you want to open and close parentheses `(` in text.
{% endhint %}

### Special attributes

#### **Hints**

**1. Info**

Used for neutral information.

```text
{% hint style="info" %}
Important information!
{% endhint %}
```

{% hint style="info" %}
Important information!
{% endhint %}

**2. Danger**

Used for irreversible changes.

```text
{% hint style="danger" %}
Danger!
{% endhint %}
```

{% hint style="danger" %}
Danger!
{% endhint %}

**3. Warning**

Used for information that requires special attention.

```text
{% hint style="warning" %}
Warning!
{% endhint %}
```

{% hint style="warning" %}
Warning!
{% endhint %}

**4. Success**

Used for successful outcomes.

```text
{% hint style="success" %}
Success!
{% endhint %}
```

{% hint style="success" %}
Success!
{% endhint %}

### Blocks of text with tabs

```text
{% tabs %}
{% tab title="This is the first tab" %}
This is a block of text with tabs!
{% endtab %}

{% tab title="And the second tab" %}
It could be used when there are different instructions for different operating systems.
{% endtab %}
{% endtabs %}
```

{% tabs %}
{% tab title="This is the first tab" %}
This is a block of text with tabs!
{% endtab %}

{% tab title="And the second tab" %}
It could be used when there are different instructions for different operating systems.
{% endtab %}
{% endtabs %}

