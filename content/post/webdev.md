+++
date = "2015-11-03T23:38:29+01:00"
draft = true
title = "Web development"
description = ""
tags = ["web", "html", "css", "stylesheet"]

+++

# Web project template

## node + gulp + git

1. Create project folder and change directory.
   The `$_` (dollar underscore) bash command variable contains the most recent parameter.
       mkdir <appdir> && cd $_

2. Inizialize `git` repository and create `.gitignore` file
       git init
       echo "/node_modules" > .gitignore

3. Create and initialize `package.json`
       npm init

4. Install `gulp` and save in `devDependencies` section of `package.json`
       npm install gulp -D

5. Install some packages for gulp tasks
       npm install browser-sync gulp-sass gulp-autoprefixer gulp-sourcemaps del -D

   Don't mind if eventually will occur the warning:

       npm WARN prefer global node-gyp@3.2.0 should be installed with -g

6. Create the `gulpfile.js`
       touch gulpfile.js

7. Edit `gulpfile.js` as:
       var gulp = require('gulp')
       var sass = require('gulp-sass')
       var autoprefixer = require('gulp-autoprefixer')
       var sourcemaps = require('gulp-sourcemaps')



# Tools

## Package manager

### [Bower](http://bower.io/)

* [Bower homepage](http://bower.io/) A package manager for the web
* [Meet Bower: A Package Manager For The Web](http://code.tutsplus.com/tutorials/meet-bower-a-package-manager-for-the-web--net-27774)

## Build tools / Task Runners

* [Grunt](http://gruntjs.com/) The JavaScript Task Runner
* [Gulp](http://gulpjs.com/) Automate and enhance your workflow
* [Broccoli](https://github.com/broccolijs/broccoli) Browser compilation library – an asset pipeline for applications that run in the browser
* [Mimosa](http://mimosa.io/index.html) a build tool for modern web development

### links

* [Task Runners, A comparison between Grunt, Gulp, Broccoli and Mimosa](http://jpsierens.com/task-runners-a-comparison-between-grunt-gulp-broccoli-and-mimosa/)
