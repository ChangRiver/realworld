# Frontend Instructor Guide

This guide will provide you with the necessary knowledge & resources required for teaching a **frontend web framework** (React, Angular2, Ember, etc) that integrates with ProductionReady.

The process of creating a frontend course is done in three steps:

1. Building the entire application
2. Breaking up the completed codebase into step-by-step checkpoints
3. Writing the course

# Building the application

## 1. Set up your initial github repo
The first thing you'll want to do is set up a github repo. We recommend creating a root level `src/` folder where your codebase will live. You can see a good example of this in the [conduit-angular repo](https://github.com/GoThinkster/conduit-angularjs-final).

## 2. Start building your app
For your convenience, we have a live API server running at X for you to build your application against. Alternatively, you can install one of the completed backend servers and run it locally.

#### Required Functionality

Like the old saying goes, a live demo is worth 10e9 words - so we recommend playing with our [live Angular based demo](put-link-here) to get a feel for the application's functionality. Use the Angular application as your north star while building out functionality; i.e. if it works a certain way in the Angular app, it should work that way in your app as well. The [conduit-angular repo](https://github.com/GoThinkster/conduit-angularjs-final) is a good reference guide should you have any questions about the feature implementations.

For your convenience, we've also included the key specs of the frontend app's functionality below.

**General functionality requirements:**

- Authenticate users via JWT (login/signup pages + logout button on settings page)
- CRU users (sign up & settings page - no deleting required)
- CRUD Articles
- CRD Comments on articles (no updating required)
- GET and display paginated lists of articles
- Favorite articles
- Follow other users

**The general page breakdown looks like this:**

- Home page (URL: /#/ )
    - List of tags
    - List of articles pulled from either Feed, Global, or by Tag
    - Pagination for list of articles
- Sign in/Sign up pages (URL: /#/login, /#/register )
    - Use JWT (store the token in localStorage)
- Settings page (URL: /#/settings )
- Editor page to create/edit articles (URL: /#/editor, /#/editor/article-slug-here )
- Article page (URL: /#/article/article-slug-here )
    - Delete article button (only shown to article's author)
    - Render markdown from server client side
    - Comments section at bottom of page
    - Delete comment button (only shown to comment's author)
- Profile page (URL: /#/@username, /#/@username/favorites )
    - Show basic user info
    - List of articles populated from author's created articles or author's favorited articles



#### Important guidelines

###### Avoid using unnecessary build tools
By default, avoid using any build tools that aren't absolutely critical for teaching real world usage of the given framework. While build tools are obviously excellent for automating routine tasks, the learners using your course have never experienced what the "routine" tasks are for building applications with your framework (otherwise they wouldn't be taking your course in the first place). Instead, manually perform tasks in the codebase -- you can always release future content that shows how to automate them :)

That being said, you will likely need to use some sort of build tool to scaffold/run the application (Gulp, Grunt, Webpack, Babel for ES6 support, etc) and that's totally fine - just don't overcomplicate things.

###### In development, the app _must_ run on localhost:4000
The backend servers run on port 3000 in development, so make sure you override the relevant config option for port number to equal 4000 in your frontend app's build tool.

###### Use the provided Bootstrap4 HTML/CSS
[Eric](https://twitter.com/ericsimons40) took one for the team and wrote all of the CSS/HTML required for your frontend application - the [conduit-sass Github repo](https://github.com/GoThinkster/conduit-sass) explains how to implement & use it in your application. Here are the important bits:

- Both Conduit specific styles and Bootstrap4 are included to ensure future updates to Bootstrap4 won't break your course
- Best practice is to install the package via NPM
- You'll need to run a SASS task in your build system to generate a browser readable CSS file

###### TDD is _not_ required
Considering these courses are largely targeting intermediate developers, we think that TDD implementations should be covered in optional supplementary courses. As such, if you want to include tests with the codebase you're more than welcome to, but it's not required.
