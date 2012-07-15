Title: Rice, Part 4
Author: Austin Yun
Date: 2012-07-15

So one of the things I was concerned about was the fact that I sorted the index
of articles to generate the home page, and then called array.reverse() on the
resulting array. Well, it turns out it's better than the alternative of parsing
the date string, [according to this test I ran on
jsperf.com](http://jsperf.com/austinyun-test1).

Well, that's one worry down.

I also tracked down the source of the annoying bug that caused an extra
paragraph tag to be added to the summary of articles on the homepage. Turns out
I was inserting the parsed markdown, paragraph tags and all, inside a set of
paragraph tags in the HTML template. Stupid. Hahahaha.
