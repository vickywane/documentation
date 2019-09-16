---
description: 'Want to make our documentation even better? First of all, thank you! This page will help you understand better our workflow and the tools we use.'
---

# Suggesting changes

To edit our docs, you must have a GitHub account. If you already have one, make sure you are logged in. If you don't, please [create one](https://github.com/join).

We also recommend you to read our style guide before submitting any changes. It serves as a reference of our writing style and our expectations for documentation.

## Understanding GitBook's integration with GitHub

We use a platform called [GitBook](https://www.gitbook.com/) to host, manage and serve our documentation. GitBook fetches files from our GitHub repository **opencollective/documentation**, reads them and converts them into the pages you can access on **docs.opencollective.org**. A generic structure of a documentation hosted on GitBook would look like this:

{% code-tabs %}
{% code-tabs-item title="Generic structure of a GitBook" %}
```text
First page
├── A group of pages

│   ├── A page
│   ├── Another page
│   ├── One more page
│   │   ├── A nested page
│   │   └── Another nested page
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Its mirror to GitHub, on the other hand, would have the following structure:

{% code-tabs %}
{% code-tabs-item title="File tree: Basic structure of a GitBook mirror repository" %}
```text
├── .gitbook/
│    └── assets/
│    │    └── an-image.png
├── a-group-of-pages/
│    ├── a-page.md
│    ├── another-page.md
│    ├── one-more-page/
│    │    ├── README.md
│    │    ├── a-nested-page.md
│    │    └── another-nested-page.md
├── README.md
└── SUMMARY.md
```
{% endcode-tabs-item %}
{% endcode-tabs %}

* The `.gitbook/assets` folder manages every file used in any page.
* The `SUMMARY.md` file tells GitBook in which order we wish to display our pages and what groups there are in our documentation.
* The `README.md` file in the main folder has the contents of the first page users see when accessing the documentation website.
* Groups of pages are controlled by folders named after the group title \(i.e. `a-group-of-pages`\).
* Nested pages have a similar structure to groups of pages; however, a `README.md` file with the contents of the parent page must be added to the folder named after the parent page title.

GitBook also created a few shortcodes for special attributes. Learn more about them reading our style guide.

## Editing existing pages

**1.** Open the page you want to edit. What you see next depends on the resolution of your screen and on whether you are viewing that page zoomed in or not.

**a.** On certain occasions, you may see a button saying **Edit on GitHub** above the **Table of Contents** on the right side of the page.

**b.** On others, you may see a GitHub icon on the top of page, next to the title and to the Table of Contents icon.

![The Welcome page as displayed on GitBook. On the right side of the page, next to the title, there are two icons: one of the GitHub logo and another designating the Table of Contents.](../../../.gitbook/assets/documentation_using_gitbook_2019-09-09.png)

**2.** Click on the GitHub icon. This will direct you to the Markdown file in which the contents of the page are stored.

**3.** Click on the pencil icon \(labeled "Edit this file"\). This will open a basic editing environment.

**4.** Make any edits you need, remembering to always format them using Markdown. To understand better GitBook's implementation of Markdown, check [their reference guide](https://docs.gitbook.com/content-editing/markdown).

**5.** When you are done making changes, scroll to the bottom and select the option **Create a new branch for this commit and start a pull request**. Write a short description of your changes and click on **Propose file change**. This will direct you to the **Pull request** page.

**6.** On the **Pull request** page, write a short comment explaining why are proposing those changes \(e.g. improving readability, covering cases that weren't mentioned, adding critical details about our platform\) and publish your pull request clicking on **Create pull request**.

**7.** Congratulations, you submitted a pull request! 🎉 Our documentation admins will review it and merge them into our documentation if approved.

## Adding new images

Assets of any kind \(images, GIFs...\) should be stored on the **.gitbook/assets** folder.

## FAQ

### I would like to suggest the creation of new pages or sections. How can I do that?

Please create an issue on our documentation repository to discuss your ideas before taking any action. This will

1. Go to [our Issue section](https://github.com/opencollective/documentation/issues) and click on **New issue**. 
2. Describe what changes you are proposing and the motivation behind them: how will them improve our documentation? How should we proceed?
3. Click on **Submit new issue**.

**I would like to add new images to existing pages. How should I proceed?**

**I submitted a pull request and a documentation admin requested changes. What should I do?**

If you have any other questions about contributing to our documentation, please reach out to **support@opencollective.com**.
