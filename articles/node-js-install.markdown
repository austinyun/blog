Title: Node JS Installation and Startup Woes
Author: Austin Yun
Date: 2012-05-28

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

That seemed to work amazingly well. Now, we go:

    npm install express -g

To install Express, which I'm not using at the moment but likely will in the future. But more importantly,

    cd ~/blog/server
    npm install wheat

Install Wheat.

I also made a dir for node modules, just in case.

    sudo mkdir /usr/local/lib/node_modules/
    sudo chown austin /usr/local/lib/node_modules/

Is that the right place to put it? Is it bad to change ownership of that dir? No idea.
