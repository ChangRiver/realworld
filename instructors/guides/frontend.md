# Frontend Instructor Guide

This guide will provide you with the necessary knowledge & resources required for teaching a **frontend web framework** (React, Angular2, Ember, etc) that integrates with ProductionReady.

The process of creating a frontend course is done in three steps:

1. Building the entire application
2. Breaking up the completed codebase into step-by-step checkpoints
3. Writing the course

# Building the application

## 1. Set up your initial github repo
The first thing you'll want to do is set up a github repo. Fork this repo, place your code in the `code` folder.

## 2. Start building your app
For your convenience, we have a live server at X for you to build your application against. Alternatively, you can install one of the completed backend servers and run it locally.

#### Feature list

The frontend application needs to have the following functionality:

give link to live demo

#### Guidelines

###### Avoid using unnecessary build tools
By default, avoid using any build tools that aren't absolutely critical for teaching real world usage of the given framework. While build tools are obviously excellent for automating routine tasks, the learners using your course have never experienced what the "routine" tasks are for building applications with your framework (otherwise they wouldn't be taking your course in the first place). Instead, manually perform tasks in the codebase -- you can always release future content that shows them how to automate them :)

That being said, you will likely need to use some sort of build tool to scaffold/run the application (Gulp, Grunt, Webpack, etc) and that's totally fine - just don't overcomplicate things.

###### Use the provided Bootstrap4 HTML/CSS
bootstrap styles/templates (explain NPM versioning)

###### TDD is _not_ required
Considering these courses are largely targeting intermediate developers, we think that TDD implementations should be covered in optional supplementary courses. As such, if you want to include tests with the codebase you're more than welcome to, but it's not required.
