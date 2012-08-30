{
    "title": "Rice, Part 2",
    "author": "Austin Yun",
    "date": "2012-06-28"
}

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

### Day 2

Alright, so after reading a lot of code and tinkering, I've got git-fs mostly
down. Phew. Turns out git-fs itself isn't that complicated, the problem came
mostly from my misunderstanding the number of arguments in callbacks due to
Wheat using the Step library.

    Git.readDir("fs", "entries", function(err, data) {});

#### Learning about routing

So with that first bit out of the way, I tried puzzling my way through MapleTree
and decided to switch to choreographer, which is... simpler, in a lot of ways.
MapleTree just does a lot of stuff I don't need. On the other hand,
choreographer hasn't been updated in a while so I may switch sometime. I dunno.
Then again, choreographer is simple enough that I don't see it breaking or
needing updates, really.

Anyway, so now that I've got the ability to grab a buffer of markdown, next up
is rendering and serving it. Hurrah.

### Day 3

Now work begins on actually being able to access different Git versions of a
file rather than just passing "fs" as the version argument to every Git
function.

Basically, it all starts with git.getHead(callback). I think.

#### A note on control flow

I'd really like to use [async](http://github.com/caolan/async) for both flow
control and obviously, asynchronous execution, but I've decided to write a first
iteration using raw callbacks and then refactor to use async at some point for
practice.

I've begun using the CSS files and touch favicons from
[Skeleton](http://github.com/dhgamache/Skeleton) with a few changes, mostly
involving me not giving a shit about IE compatability. Oh yeah, and I replaced
the default favicon with Twilight Sparkle, of couse.

OK, so I've run into a show-stopper of a problem even though everything is going
well coding wise.

Basically, git-fs, the cornerstone of the engine, won't work on Heroku. And it's
not a problem with git-fs, rather, the problem is that _stuff pushed to Heroku
is not a git repository._

Sooooooooo, I guess I'll have to fork rice in order to not use git-fs and ditch
the automatic versioning feature if I want to deploy on Heroku. Either that, or
use a no.de instance (might work, not sure, proably will since wheat runs
there), but man, is that a bummer.

On the plus side, I've got a lot of the Jade templating stuff figured out, so
yay about that.

### Day 4

Considering going back to MapleTree. The partial matches and stuff might be
useful. Also, it's in active development, unlike Choreographer.

Also, very strongly considering switching Jade for doT, which is about 100,000
times faster. But then the name wouldn't make sense, hahahaha. Oh well. I'm a
big fan of purely declarative templates. Separating UI from logic and all that.

However, doT doesn't seem to be in active development, unlike Handlebars, which
is the other alternative. :\

My left wrist is starting to hurt. Need a new keyboard. Got to remember to use
the right ALT key too. May rebind Capslock from CTRL to ALT since I'm using ALT
more it seems.

You know, I never use the right modifier keys? It's a bad habit, and probably
one I should break.

Capslock -> ESC might work too, since I'm a Vim user and all. But I'm 90% sure
my recent wrist pain is from left ALT+1/2/3/4 all the time.

#### POSSIBLE SOLUTION

Oh lawd, I just had a brilliant idea.

1. Make rice child_process.exec git clone the contents of the blog, but not the
   blog engine (would have to be hosted in a different repo with just articles
   and static files and stuff). Oh wait, maybe I should put it in server.js
   before rice() is executed. That keeps them separated.
2. That will handle the problem of not having a git repo for git-fs to use.
   Hopefully. I'll have to experiment with it later.

So now I have indeed replaced Jade with doT. Name no longer makes sense. Sigh.

Anyway, I started on the parser. At the moment it's basically a copy/paste of
the markdown preprocessing function from [wheat's
data.js.](http://github.com/creationix/wheat/blob/master/lib/wheat/data.js#L8)

Having a lot of fun.

### Day 5

Alright, I've got pretty much up and running with doT and marked. Awwwwww yeah.
Also, rice now stores the compiled doT index and article templates in memory
after the first time, so that the template itself doesn't have to be compiled
every time.

Now I've basically got to implement the part where rice builds a list of
articles sorted by date to make the index object.
