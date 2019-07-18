


# How to contribute to Open collective
 
We're happy to see you contributing to our project through our bounty program! 
To successfully contribute, we recommend you go through the following guide. 

## Technical Requirements

While some of our issues are simple and easy to fix, it is important to have some basic programming experience with the technologies and tools we use.

#### Tools

- **Git & Github** - It is important to know how to clone, commit, open a PR using Git with GitHub. To learn how to use Git & Github checkout the following quick tutorials:
                
     - [Introduction to git](https://www.freecodecamp.org/news/what-is-git-and-how-to-use-it-c341b049ae61/)  
     - [Introduction to github](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners)
     - [Popular git command and how to use them](https://rogerdudler.github.io/git-guide/)
     - [Git command indept](https://medium.com/@george.seif94/a-full-tutorial-on-how-to-use-github-88466bac7d42)
     

#### Language & Frameworks

- **JavaScript/Nodejs** - We recommend having basic experience working with JavaScript/Nodejs as Open Collective is written in Javascript (Frontend & Backend). Checkout these free and quick JavaScript & Nodejs tutorials: 
    - Javascript
       - [Introduction to basic principles of Javascript ](https://eloquentjavascript.net/)
       - [Introduction to Javascript - w/ Advanced concepts](https://javascript.info/)
       - [An interactive Javascript tutorial](https://www.learn-js.org/)

   - Nodejs
       - [Quick introduction to Nodejs](https://www.tutorialspoint.com/nodejs/nodejs_quick_guide)
       - [Introduction to Nodejs - w/ quizzes](https://www.tutorialsteacher.com/nodejs/nodejs-tutorials)
       - [When, how and why to use Nodejs](https://www.netguru.com/blog/use-node-js-backend)
       - [Differences between Javascript and Nodejs](https://www.educba.com/javascript-vs-node-js/)
     
     
- **GraphQL** - Our API uses GraphQL  powered by [Sequelize](http://docs.sequelizejs.com/manual/getting-started.html) and [PostgreSQL](https://www.postgresql.org/). Understanding how graphql works is important to contributing or fixing majority of the issues on our API. To learn more about graphql checkout these tutorials & articles: 
   
   - [What is GraphQL and how to use it](https://www.howtographql.com/)
   - [Basic concept of GraphQL](https://medium.com/@kalin.chernev/the-guide-to-learn-graphql-i-wish-i-found-few-months-go-97f9d9ca6f12)
   - [Getting GraphQL running](https://www.freecodecamp.org/news/a-beginners-guide-to-graphql-86f849ce1bec/)
   - [Practical GraphQL tutorial](https://blog.digitalocean.com/learning-graphql-by-doing/)
   
- **React & Nextjs** - Our Frontend is built with React and Nextjs, to contribute to issues on our frontend, be sure you have basic understanding of React and how it works with Nextjs. To learn more about React and Nextjs checkout the following links:
     - React
         - [Basic React Concepts](https://blog.usejournal.com/a-beginners-guide-to-react-36b19943d58f)
         - [The Beginner react roadmap - path to mastering react](https://www.freecodecamp.org/news/learning-react-roadmap-from-scratch-to-advanced-bff7735531b6/)
         - [React Official documentation](https://reactjs.org/tutorial/tutorial.html)
     - Nextjs
         - [Basic introduction to Nextjs](https://medium.com/front-end-weekly/next-js-what-is-it-9cb2f4af8f27)
         - [Nextjs Official Documentation](https://nextjs.org/docs#how-to-use)
         - [Basic concepts in Nextjs](https://www.freecodecamp.org/news/an-introduction-to-next-js-for-everyone-507d2d90ab54/)
         - [Introduction to Nextjs - w/ Advanced concepts](https://flaviocopes.com/nextjs/)

## Project Structure

The project core repositories are divided into three:

- **[opencollective/opencollective](https://github.com/opencollective/opencollective)** - Here we manage our issues and discuss with the communities on things we're working on. Our issues are well labelled, issues to fix have complexity label, we recommend starting with simple issues ( [`complexity -> simple`](https://github.com/opencollective/opencollective/issues?q=is:issue%20is:open%20label:%22complexity%20%E2%86%92%20simple%22)).

- **[opencollective/opencollective-frontend](https://github.com/opencollective/opencollective-frontend)** - This repository contains our frontend code. You can find more information in the setup section of this guide.
- [**opencollective/opencollective-api**](https://github.com/opencollective/opencollective-api) - This contains our api code. If you enjoy working on backend, you can set up our api locally, to learn about setting it up, checkout the setup section.


## Project setup
This section explains how you can get Open Collective running locally on your computer.

### Frontend
Setting up the frontend is straight forward and we've provided a comprenshive guide in a seperate document that explains how to set up the project. 

#### Setup guide
> https://github.com/opencollective/opencollective-frontend/blob/master/README.md
 
NOTE: If you're only interested in contributing to frontend code, you don't need to setup the API.

### API

The API setup is simple but requires more effort than the frontend as the API requires installing [PostgreSQL](https://www.postgresql.org/download/) and [PostGIS](https://postgis.net/install/) Extension. It is important to be aware that you might experience difficulty setting up the API on a Windows environment, we recommend using a Unix environment. (We're currently working to make it easier on windows)

Just like the frontend, we have a seperate document for the setup.

#### Setup guide

> https://github.com/opencollective/opencollective-api/blob/master/README.md

## Others

### Design Contribution

Like to contribute to our design? Checkout our design contribution guidelines:

> https://docs.opencollective.com/help/design/untitled


### Commit convention

Before you make your first commit, read through our commit convention provided in the link below:

> https://github.com/opencollective/opencollective-frontend/blob/master/CONTRIBUTING.md
> 

### Bounty Program
We recommend you learn more about our bounty program through the link below:

> https://docs.opencollective.com/help/developers/bounties

### Ask for Help

You stuck or you have a question without answer in the docs? Join our slack #engineering channel through the link below to ask our team:

> https://slack.opencollective.com/

We're trying our best to make our documentation better, we encourage you give suggestions on how we can improve it and feel free to correct any grammatical errors. Checkout our full documentation in the link below.

> https://docs.opencollective.com/

