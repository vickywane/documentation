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

![Screenshot of our Welcome page. A GitHub icon along with the text "Edit on GitHub" is seen above the Table of Contents.](/.gitbook/assets/Contributing_Documentation_Suggesting_changes_GitHub_Icon_With_Text_2019_09_16.png)

**b.** On others, you may see a GitHub icon on the top of page, next to the title and to the Table of Contents icon.

![Screenshot of our Welcome page. On the right side of the page, next to the title, there are two icons: one of the GitHub logo and another designating the Table of Contents.](/.gitbook/assets/Contributing_Documentation_Suggesting_changes_GitHub_Icon_Small_2019_09_16.png)

**2.** Click on the GitHub icon. This will direct you to the Markdown file in which the contents of the page are stored.

**3.** Click on the pencil icon \(labeled "Edit this file"\). This will open a basic editing environment in which you are able to costumize aspects like line wrap and indentation.

![Screenshot of a version of our Contributing page on GitHub showing the Edit this file button as a pencil icon.](/.gitbook/assets/Contributing_Documentation_Suggesting_changes_Edit_this_file_2019-09-16.png)

**4.** Make any edits you need, remembering to always format them using Markdown. To understand better GitBook's implementation of Markdown, check [their reference guide](https://docs.gitbook.com/content-editing/markdown) and our style guide.

**5.** When you are done making changes, scroll down and write a short description of your changes. Select the option **Create a new branch for this commit and start a pull request** and click on **Propose file change**. This will direct you to the **Pull request** page.

![Screenshot of the Commit changes box. There are boxes for a brief description of the changes, an extended one, a selection menu for email addresses to associate with the commit, options to commit directly to the current branch or to create a new branch and a pull request (which opens an option to name your branch as you like) and buttons to either Propose file change or Cancel.](/.gitbook/assets/Contributing_Documentation_Suggesting_changes_Commit_and_propose_2019-04-29.png)

**6.** On the **Pull request** page, write a short comment explaining why are proposing those changes \(e.g. improving readability, covering cases that weren't mentioned, adding critical details about our platform\) and publish your pull request clicking on **Create pull request**.

![Screenshot of the Pull request page. It shows a box for the title of the Pull request, another for any comments. Below them, there's a Create pull request button.](/.gitbook/assets/Contributing_Documentation_Suggesting_changes_New_pull_request_2019-04-29.png)

**7.** Congratulations, you submitted a pull request! 🎉 Our documentation admins will review it and merge them into our documentation if approved.

## Adding new images

Assets of any kind \(images, GIFs...\) should be stored on the **.gitbook/assets** folder.

**1.** Clone our documentation repository to your account.

**a**. Click on the **Fork** button at the top of the page.

![Screenshot of the documentation repository showing the Fork button.](/.gitbook/assets/Contributing_Suggesting_changes_Repository_Fork_Button_2019_09_16.png)

**2.** On your copy of the repository, create a new branch by clicking on **Branch: master**, writing **new-assets** and selecting **Create branch: new assets**.

 ![GIF of the process to create a new branch.](/.gitbook/assets/Contributing_Documentation_Suggesting_changes_New_branch_2019-09-16.gif)

**3.** Click on the **.gitbook/assets** folder and then click on **Upload files**. You can drag and drop any files you wish to add or find them with your file manager clicking on **choose your files**. Commit your changes.

![GIF of the process to upload new files.](/.gitbook/assets/Contributing_Documentation_Suggesting_changes_Upload_assets_2019-09-16.gif)

**4.** GitHub will automatically detect your new changes and give you the option to **Compare and pull request**. Click on it.

**5.** Create your pull request normally. The base repository should be **opencollective/documentation** using the **master branch** as the base and the head repository should be **your fork** using the **new-assets** branch as a comparison.

![Screenshot of the Open pull request page showing a comparison between the base repository (opencollective/documentation on the master branch) and the head repository (your fork on the branch new-assets)](/.gitbook/assets/Contributing_Suggesting_changes_Open_pull_request_fork_2019_09_16.png)

## Adding new sections, pages and subpages

{% hint style="warning" %} Please create an issue on our documentation repository to discuss your ideas before taking any action.

1. Go to **[our Issue section](https://github.com/opencollective/documentation/issues)** and click on **New issue**. 
2. Describe what changes you are proposing and the motivation behind them: how will them improve our documentation? How should we proceed?
3. Click on **Submit new issue**.

{% endhint %}

**0.** Follow the same procedure to make a copy of our documentation repository as described on the **Add new images** section. Name your branch **new-pages**, **new-section** or **new-subpages** accordingly.

**1.** To add a new file or folder, click on **Create new file**.

{% hint style="info" %} To create a Markdown file, remember to write the name of the file and add the `.md` extension. {% endhint %}

**a.** If you want to add a new page to an existing section of the documentation, click on the proper folder and then click on **Create new file**. Name your Markdown file and start writing.

{% hint style="info" %} Remember: Your page will be named after the first h1 heading on your Markdown file, and not the name of the file. {% endhint %}

**b.** If you want to add a new section to our documentation, click on **Create new file** directly. Write the name of the section and press `/` as many times you need. Add either a `README.md` file or a normal Markdown file with any name you want.

{% hint style="info" %} Remember: `README.md` creates a page with the same name of your new folder. Markdown files with any other name will create pages with a title using the first h1 heading. {% endhint %}

![GIF showing how to add new folders and files.)](/.gitbook/assets/Contributing_Documentation_Suggesting_changes_New_folder_and_files_2019-09-16.gif)

**2.** GitHub will automatically detect your new changes and give you the option to **Compare and pull request**. Click on it.

**3.** Create your pull request normally. The base repository should be **opencollective/documentation** using the **master branch** as the base and the head repository should be **your fork** using the right branch as a comparison.

![Screenshot of the Open pull request page showing a comparison between the base repository (opencollective/documentation on the master branch) and the head repository (your fork on the branch new-assets)](/.gitbook/assets/Contributing_Suggesting_changes_Open_pull_request_fork_2019_09_16.png)

If you have any other questions about contributing to our documentation, please reach out to **support@opencollective.com**.
