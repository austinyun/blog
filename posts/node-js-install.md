Title: Node JS Installation and Startup Woes
Author: Austin Yun
Date: 2012-05-28

### Installing Node via NVM
So right now I'm giving nvm a try, which is the node version manager.

First I uninstalled the apt version of node

    sudo apt-get remove node

Then I gave nvm a try according to the instructions, only to have it blow up in my face for not having OpenSSL. Turns out I need the openssl-dev package for this to work.

    sudo apt-get install openssl-dev
    git clone git://github.com/creationix/nvm.git ~/.nvm
    echo ". ~/.nvm/nvm.sh" >> ~/.bashrc

Exit and reopen the terminal:

    nvm install v0.6.18
    set default node
    nvm alias default v0.6.18

Everything should be working. Type

    node --version
        v0.6.18

### Installing Express
That seemed to work amazingly well. Now, we go:

    npm install express -g

To install Express, a web framework for Node, which I'm not using at the moment but likely will in the future. Awesomely enough, Node comes with it's own package manager, npm, and the syntax is very basic. The only thing of note is that the -g tag at the end installs the given package globally. You would do this for things that have their own command associated with them, like express does.

### The blog engine
So if you haven't been to [howtonode][1] you really should check it out, if for no other reason than to check out a blog that's running on Wheat, a blog engine written in Node. In fact, Tim Caswell of [howtonode][1] wrote Wheat, but unfortunately kind of skimped on the documentation. His suggestion to get up and running is to just clone the howtonode GitHub repository.

    cd
    git clone git://github.com/creationix/howtonode.org.git
    cp howtonode.org/ blog/
    rm blog/authors/* blog/articles/*


That should make a directory called howtonode.org wherever you called the git command from, and copy it all to your own directory called blog. That way you can see a fully setup version and then add stuff to your own. Check out the examples for a sample article and author page, then do

    cd ~/blog/server
    npm install wheat creationix stack

Install Wheat, and two other things this particular blog depends on. This is obviously more important because it's what's powering this blog right now. And it's the whole reason I'm writing this. At this moment, I have no idea whether the creationix or stack packages are actually necessary. Stack seems to be a piece of middleware that does something similar to connect, another node package. Shrug.

Anyway, do,

    node ~/blog/server/server.js

And point your browser to localhost:8080 to see your blog, which should look exactly like howtonode.org. For obvious reasons.

[1]: http://howtonode.org "How To Node"
