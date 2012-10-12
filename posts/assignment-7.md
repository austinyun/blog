{
    "title": "Java II Assignment #7",
    "author": "Austin Yun",
    "date": "2012-06-05"
}

Today, I have to implement a version of Hangman, without using the ACM Graphics package.
That's about it.
Everything else is flexible.
Yay.

# Day 1
So far all I've got up is a HangmanMain.java and HangmanGUI.java.
I've got a lot of thinking to do about how I'm going to do this, and of course I've got some Swing documentation to read.

# Design phase
* DISPLAY
    * One window, split into two frames
    * Top: Hangman display, Bottom: "Keyboard"
        * The hangman will have a drawing of a stick figure that gets filled in progressively as you make mistakes, along with the classic set of underlines instead of letters
        * The keyboard will be A-Z? Probably better than QWERTY
        * Clickable or input a letter by typing
        * Accepted/correct letters will turn green, rejected ones red.
* IMPLEMENTATION
    * Sets guarantee that there's only one of each element, so I might use that for the keyboard, letters attempted, letters accepted, and maybe valid letters
    * Array for the word itself?
        * Has the advantage of being given a set length, can initially set every element to "_"
        * Don't know how to check how many instances of a given letter occur in the word and at what index though
