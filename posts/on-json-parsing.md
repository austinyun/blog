{
    "title": "On JSON Parsing",
    "author": "Austin Yun",
    "date": "2012-08-29"
}

In my constant refactoring of [Rice][1], I decided to break from [Wheat][2] in another way by changing the format of post metadata.
Instead of plaintext key value pairs of the form `key: value`, I decided to just stick a JSON object at the start of the file.

That lead me to need to find a good JSON identifier/parser, and after a while I decided to use a solution I found by [ThiefMaster on StackOverlow][3].
IMO it's well suited to my needs for several reasons.
One, in most all-text blog posts, it will correctly identify the JSON object on the first time through the loop, as there shouldn't be many '}' characters (this post will be an exception because of what I just typed!).
Two, it won't utterly fail otherwise, and in fact will succeed with some pretty whacky input.
And third, this way I don't rely on an arbitrary division between where the metadata ends and the post begins, like the '\n\n\n' that I was using before.

Anyway, with ThiefMaster's permission I made a few modifications and turned that little piece of code into it's own NPM module called (in a stunning display of creativity), [json-finder][4], available now.

PS: Another bonus is that the way the function works is fairly flexible because it returns the object, and the index of the start and end of the object in the original string, so you're free to do with the original string as you please.

[1]: https://github.com/austinyun/rice
[2]: https://github.com/creationix/wheat
[3]: http://stackoverflow.com/a/10574546/298479
[4]: https://npmjs.org/package/json-finder
