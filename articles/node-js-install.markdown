Title: Node JS Installation and Startup Woes
Date: 2012-05-28

The node package that comes with Ubuntu 12.04 is... well, it works, but npm doesn't. Either that, or I just have no idea what I'm doing. It could very well be the latter. So right now I'm giving nvm a try, which is the node version manager.

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

That seemed to work amazingly well. Now, we go:

    npm install express -g
    npm install wheat -g

To install Express and Wheat globally. I also made a dir for node modules, just in case.

    sudo mkdir /usr/local/lib/node_modules/
    sudo chown austin /usr/local/lib/node_modules/

Is that the right place to put it? Is it bad to change ownership of that dir? No idea.
