Title: Java II Assignment #6
Author: Austin Yun
Date: 2012-05-31

## The Problem

Make a binary search tree class for a game of 20 questions (though not necessarily with a depth of 20), that can do the following:

* Using a set of classes already provided:
* Save the BST to a text file in preorder traversal order
* Load a BST from a text file in preorder traversal order This is possible because every node has either 0 or 2 branches.
* Ask questions according to each node in the BST, going down the yes or no path according to user input
* If you stump the computer, it asks what object you were thinking of, a question to distinguish it from what its guess was, and the answer to your question, and then edits the BST appropriately.

## My solution

This one I found fairly simple. Not necessarily easy, but I didn't get outright stuck on any part of the problem, although it took me embarrassingly long to write the method that recursively builds a BST from a text file.

[Here's my QuestionTree.java](https://github.com/austinyun/C-Sci/blob/master/C-Sci-143/Assignment%206/src/QuestionTree.java)

The full project with text files and the provided classes are available too. Just go up a level on GitHub.
