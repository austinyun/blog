{
    "title": "Java II Assignment #5",
    "author": "Austin Yun",
    "date": "2012-05-22"
}

For assignment #5 I'm supposed to make a game called (lazily enough) the Assassins Game.
Basically, you have a list of random people, who have a random target, and a random person who is targetting them.
They all kill eachother until only one person is remaining, and that person is the winner.

[Link to the repo][1]

# Attempt 1
I sat down and tried to bang out a solution without any real thought.
Surprise surprise, it didn't work.
Oh well. I'm going to take a shower and think it through.
First, stuff I know.

* It's implemented as a Linked List.
* Every node in the list is an assassin, who has a target and a killer, analagous to next and previous. Therefore it's a doubly linked list.
   * However, it may be unnecessary to implement the 'previous', because I don't see any requirement to traverse the list in the opposite direction.
* The list is intended to be circular.

Given those points, it's clear that basically what I need to is make a circular singly linked list, and implement kill, which basically skips the node.next() forward one space.
But there's the graveyard thing too.
Eh.
I guess kill also adds the removed node's name to the graveyard, which might as well be implemented as a comma or newline delimited string or something, because the only things required of the graveyard are checking if a name is in it, and printing the names of everyone who's in it.

Actually, the graveyard also includes who killed who.
OK, well in that case I suppose I have to reuse the node objects and use node.getKiller() and stuff.
So what do I do, make another linked list for the graveyard?
Meh.
I'll worry about that part later.
First, how to construct a circular linked list, and implement get, kill, next, and all that.

# Attempt 2

OK I think I got everything working.
Yay.
The kill method is a little ugly though, but I can't think of a way to clean it up at the moment.

[1]: http://github.com/austinyun/C-Sci/tree/master/C-Sci-143/Assignment%205/src
