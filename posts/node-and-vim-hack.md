Title: Node.js and Vim Hack
Author: Austin Yun
Date: 2012-05-30

If you're hacking around building a NodeJS server in Vim, the following (extremely dangerous, don't say I didn't warn you) keybindings in your .vimrc might help:

    autocmd Filetype javascript map <F3> :w<CR>:!nohup node % >> output.log &<CR>:!chromium-browser localhost:8080<CR><CR>

    autocmd Filetype javascript map <F4> :!killall -2 node<CR>

The first one binds the F3 key to write the current file, and then runs nohup node on the current file (%) and redirects output to the file output.log. You need nohup so that Vim isn't stuck watching stdout from the node process. And then it opens Chromium at localhost port 8080, which you could obviously change to be whatever port your server is listening on.

The second kills all node processes. Don't blame me if something goes wrong here.
