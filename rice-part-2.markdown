Title: Rice, Part 2
Author: Austin Yun
Date: 2012-06-28

Step 1: Understanding
=====================

So obviously the first part of recreating Wheat is understanding just what the
hell Wheat does. Unfortunately for me, it seems the Git integration part of
Wheat is the most complicated by far. I'm currently reading through Caswell's
code following the nested function calls through various files and trying to
figure out what exactly is going on in order to read a single file. I know the
main file, wheat.js calls Git(process.cwd()), then something happens, and then
Renderers.article, for example, is called, and then Data.fullArticle.

I believe my next step should be to see what the result of line 68 of wheat.js
is.
    var match = url.pathname.match(route.regex);
One of my big hangups is that I'm trying to figure out how git-fs determines
what the SHA/version of a file is. And every other call made to git-fs depends
on that. Lol.
