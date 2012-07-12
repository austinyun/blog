Title: Rice, Part 1
Author: Austin Yun
Date: 2012-06-28

Today, I (re)-started my first real Javascript/NodeJS project. [I'm calling it Rice.](http://github.com/austinyun/rice)

### What is it?

Rice is a pseudo-clone of the [Wheat blog engine](http://github.com/creationix/wheat), intended to be more minimal and modern, mainly by using [Jade](http://github.com/visionmedia/jade) to handle templating and markdown conversion.

That explains the name, of course. Terrible pun: Wheat + Jade = Rice.

Anyway, for those unfamiliar with Wheat, it's a wonderful minimalist blog engine written by [Tim Caswell](http://howtonode.org) that uses a Git repo of articles stored in .markdown format as its backbone. Pretty cool stuff, and very simple.

### So what am I doing?

I'm basically going to be re-writing from scratch a simulacrum of Wheat's functionality in my own way.

### Project Goals

* Leverage existing Node modules for as much functionality as possible
  * I like not reinventing the wheel. Plus, my wheels suck compared to other people's lol. I'm not so arrogant that I think I can do everything better.
  * Be lean (and I mean tiny), quick to setup, easily deployable to Heroku and other cloud services
* Run my personal blog
* Learn some stuff about Javascript / Node
* OPTIONAL: Generate and serve static HTML somehow?
  * I know Jekyll does this, I should check out how

### Project Outline

* Blog entries stored as .markdown files in a Git repository
* Walk through the articles directory
* Generate routes based on article titles
* Generate HTML by plugging the article markdown into a Jade template

### App Components

* *Jade* is the backbone of the whole thing, providing templates and markdown parsing
* *MapleTree* is a routes generator for Node that I'll be using (heard about it on the Nodecast)
* *Union* is a streaming, minimal alternative to Connect. I'm not entirely sure I'll need it.

### Development Environment

I'm mostly going to be doing this in my Arch Linux setup, using Vim (my love) or Emacs (which I'm kinda learning).

I'm going to try out [Nodemon](http://github.com/remy/nodemon) as well. Autoreloading during development sounds pretty badass.

I don't know if I'm going to use a testing framework (unlikely) or roll my own tests (more likely), but I should definitely implement tests at some early point in development.
