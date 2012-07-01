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

Day 2
-----

Alright, so after reading a lot of code and tinkering, I've got git-fs mostly
down. Phew. Turns out git-fs itself isn't that complicated, the problem came
mostly from my misunderstanding the number of arguments in callbacks due to
Wheat using the Step library.

    Git.readDir("fs", "entries", function(err, data) {});

### Learning about routing

So with that first bit out of the way, I tried puzzling my way through MapleTree
and decided to switch to choreographer, which is... simpler, in a lot of ways.
MapleTree just does a lot of stuff I don't need. On the other hand,
choreographer hasn't been updated in a while so I may switch sometime. I dunno.
Then again, choreographer is simple enough that I don't see it breaking or
needing updates, really.

Anyway, so now that I've got the ability to grab a buffer of markdown, next up
is rendering and serving it. Hurrah.

Day 3
-----

Now work begins on actually being able to access different Git versions of a
file rather than just passing "fs" as the version argument to every Git
function.

Basically, it all starts with git.getHead(callback). I think.

### A note on control flow

I'd really like to use [async](http://github.com/caolan/async) for both flow
control and obviously, asynchronous execution, but I've decided to write a first
iteration using raw callbacks and then refactor to use async at some point for
practice.
