Title: Challenge: Array Incrementing
Author: Austin Yun
Date: 2012-08-03

I ran across a [very interesting blog post][1] while browsing [Hacker News][2] the
other day. The author goes over one of his favorite intervew questions to pose,
which is a really fun problem, because it's fairly simple, but has a lot of
hidden complexities in it. Here's his actual definition of the problem:
```
add1 - increments items in an array matching specified value

param: arr - array of integers to manipulate
param: val - integer, value to increment
param: n   - integer, control value specifying behavior of manipulation
  n == 0 means increment all occurrences of val

  n > 0  means increment up to n occurrences of val
         from left-to-right (forward)

  n < 0  means increment up to n occurrences of val
         from right-to-left (backward)

return: arr with proper values incremented
```

Given that most of the solutions given were variations on the theme of looping
through the array and changing the elements, I decided to channel Rich Hickey
and try to decompose the problem into simpler pieces, and write composable pure
functions to combine together into the final solution.

[Here's how I did it.][3]

First, my analysis of the problem:

* My attempt to decompose it into smaller pieces is
    * Traverse the array from either the left or the right
    * Increment each element if the value matches the one passed
        * But only do this n times!

I tried to write a function `function(f, g, bool)` that would apply f if bool
were true, and g if bool were false, and pass it a function `n_times` as the
bool part.
```
function n_times(n) {
    var count = n;
    return function() {
        if (count >= 0) {
            count -= 1;
            return true;
        }
    return false;
    }
}
```

The problem is that the counter in n_times decrements no matter what, and I want
the counter to only decrement if I incremented a value! So I ended up writing a
different function that takes care of most of the logic as follows:
```
function choose(f, g, n) {
    var count = n;

    return function() {
        var args = Array.prototype.slice.call(arguments);
        if (count >= 0) {
            count -= 1;
            return f.apply(null, args);
        }
        return g.apply(null, args);
    }
}
```

So here we have a function of two functions, f and g, and an integer, n, that
returns a function that will apply f to its arguments n times, and then apply g
to its arguments from there out.

Then, I need two helpers:
```
function increment_if_match(value, item) {
    item = item === value ? item + 1 : item;
    return item;
}

function identity(x) { return x; }
```

Both pretty much do what they say on the tin. Now you compose the the pieces,
```
var incrementer = increment_if_match.bind(null, 1);
var magic = choose(incrementer, identity, 5);
```

And you have a function that will increment the thing it's passed in if it's
equal to 1, five times, and from then on leave it alone.

The other big piece of the problem is going through the array from either side.
Well, as it turns out, a simple fold / foldr saves the day.

[For kicks, here's my original solution.][4]

[1]: blog.jazzychad.net/2012/08/01/array-iteration-problem.html
[2]: news.ycombinator.com
[3]: https://github.com/austinyun/challenges/blob/master/array-iteration-interview-problem/add1.js
[4]: https://gist.github.com/3243470
