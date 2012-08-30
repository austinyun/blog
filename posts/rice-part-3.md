{
    "title": "Rice, Part 3",
    "author": "Austin Yun",
    "date": "2012-07-08"
}

So now that the initial featureset is complete, I wonder what step I should take
next? Do I add tests for behaviour? Do I refactor the existing code? Or do I
work on adding the missing features?

I know that the TDD people would say that I'm waaaay behind on tests anyway,
given that they think you should write tests _first_. But I'm not entirely sure
how to write tests for the blog engine.

One bug I know of for sure is that for some reason the markdown parser (marked)
is not properly removing newlines. There's no visible effect on the end result
as far as I can tell, but it kind of bothers me, lol.

Obviously there's a lot of stuff I could do to as far as the HTML templates go
or CSS, but I consider that completely separate from the blog engine.

Which reminds me, one thing I could possibly do is further separate the logic of
the blog engine from the actual Github repository. My idea is to pass the name
of a Git repo as an argument to the main rice() function, which would then upon
initialization, pull (or perhaps clone) a repo containing the articles and
templates and stuff.

So, the todo list I guess is:

* Refactor
    * Restructure the code to flow logically and be composed of discrete parts
    * Make sure variable and function names are descriptive
    * Add comments where needed
    * Possibly implement more pieces with async.js
    * Make things more functional if possible (in the functional programming
      sense, not the 'it actually works' sense)
* Write tests
    * But that means I have to either choose a test framework or... a non-test
      framework.
* Implement the git-fs functionality (ability to look up past versions of an
  article by SHA)
* Have the ability to read articles from a bare repo so that it can be pushed to
* Or find out how to add a post-commit hook to a repo on Github so that when an
  article or article update is pushed to the Github repo, it triggers a pull on
  the server repo.
