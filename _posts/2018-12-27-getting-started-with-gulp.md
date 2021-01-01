---
layout: post
title:  "Getting Started with Gulp"
author: mus
categories: [Web Development, Tutorial ]
image: assets/images/post/2018/gulp.jpg
tags: [Web Development, Tutorial, Gulp]
---
Gulp is an amazing tool that helps you with some tasks when it comes to the web development especially in front-end tasks. This article will help you to use gulp, so you can begin exploring using gulp by yourself. Gulp is usually used in some tasks like:

- Using preprocessing like Less or Sass
- Reloading the browser automatically when a file is saved
- Optimizing assets like Image, JavaScript and CSS

Before we begin to dive into gulp, we will talk about why we using Gulp.


## Why Gulp?
Gulp is a tool for running tasks for building a website, it can also be referred to `build tools`. The main difference from gulp and the other is how you to configure a workflow with them. Gulp tends to run faster and it has shorter and simpler than grunt.

## Installing Gulp
You have to install Node.js (Node) in your computer before you install Gulp. If you don’t already have Node.js installed, you can get it by downloading the installer from the website. After installing Node, you can install Gulp by using the following command in the command line:


```bash
$ sudo npm install gulp -g
```

The command npm install is used for installing gulp onto your computer using `npm` (Node Package Manager). The `-g` option tells to install gulp globally onto your computer. It’s mean that you can use the command gulp anywhere from your computer. We need `sudo` to install gulp because it need administrator right to install globally.

Now gulp has already installed. Let’s start a project using gulp.

## Create Gulp Project

First, we need to create a project’s folder for the project that we are going to create. For example, we make a new project folder (gulp). Enter to the new project and run this command.

```bash
$ npm init
$ npm install gulp --save-dev
$ npm i -g gulp-cli
```

The command npm init creates a json package file package.json for your project which stores about the project information, it’s same like the dependencies used in the project (Gulp is an example of a dependency). And then we can install Gulp into the project by using the second command. We’ve already added –save-dev on the last command, which tells the computer to add gulp as a dev dependency in package.json.

When the command has already finished executing, you can check on the project folder, you will see that Gulp has created a node_modules folder in the project. You can see a folder gulp in the node_modules folder.

Now, We’re ready to start working with Gulp. Before we start, we have to be clear on how we’re going to use Gulp for the project. This is a directory structure for this article, we will use it for generic webapp.

```pre
|- app/
  |- css/
  |- fonts/
  |- images/
  |- index.html
  |- js/
  |- scss/
|- dist/
|- gulpfile.js
|- node_modules/
|- package.json
```

We have to keep this directory structure in mind when we work on our Gulp. In this directory structure, we are going to use the app folder for development and the dist (“distribution”) folder is used to contain optimized files for the production site.

Since app is used for development purposes, all our code will be placed in app folder.
Now, let’s start creating your first Gulp task in gulpfile.js, this file stores all Gulp configurations.

#Starting with gulp task
The first step is require gulp and use this statement on gulp file. It tells Node to look for a package with name gulp in node_modules folder. Once the package is found, we assign its contents to the variable gulp. Now, we can begin to write a gulp task with this gulp variable.

create file `gulpfile.js` and write this code on the file

```javascript
var gulp = require('gulp');﻿

gulp.task('hello', function() {
console.log('Hello Muse');
});
```

To try this gulp, let’s create a task that says Hello Muse !. You can run this task in your command line

```bash
$ gulp hello
```


Gulp tasks are more complex than this. It usually contains two additional Gulp methods, with a variety of Gulp plugins. This is an example of real gulp task may look like:

```javascript
gulp.task('task-name', function () {
 return gulp.src('sourceFiles') // Get source files using gulp.src
 .pipe(gulpPlugin()) // Sends it to the gulp plugin
 .pipe(gulp.dest('destinationFolder')) // Send outputs file to the destination folder
})
```


You can see now, a real task in gulp takes two additional gulp methods, gulp.src and gulp.dest. gulp.src tells to the gulp what files to use for the task, while gulp.dest tells Gulp where to output the files once the task is completed.

Now, we are ready to build a real task from gulp. This tutorial will be continued on the next articles
