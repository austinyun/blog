Title: C Sci 143 Assignment #5
Date: 2012-05-22 Tuesday

## The Problem

Assassin Game

## Attempt 1

I sat down and tried to bang out a solution without any real thought. Surprise surprise, it didn't work. Oh well. I'm going to take a shower and think it through. First, stuff I know.

* It's implemented as a Linked List.
* Every node in the list is an assassin, who has a target and a killer, analagous to next and previous. Therefore it's a doubly linked list.
   * However, it may be unnecessary to implement the 'previous', because I don't see any requirement to traverse the list in the opposite direction.
* The list is intended to be circular.

Given those points, it's clear that basically what I need to is make a circular singly linked list, and implement kill, which basically skips the node.next() forward one space. But there's the graveyard thing too. Eh. I guess kill also adds the removed node's name to the graveyard, which might as well be implemented as a comma or newline delimited string or something, because the only things required of the graveyard are checking if a name is in it, and printing the names of everyone who's in it.

Actually, the graveyard also includes who killed who. OK, well in that case I suppose I have to reuse the node objects and use node.getKiller() and stuff. So what do I do, make another linked list for the graveyard? Meh. I'll worry about that part later. First, how to construct a circular linked list, and implement get, kill, next, and all that.
