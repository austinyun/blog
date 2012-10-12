{
    "title": "Arch Linux Guide",
    "author": "Austin Yun",
    "date": "2012-06-25"
}

I've spent enough time recently installing and configuring a brand new [Arch Linux](http://www.archlinux.org) system to be my development environment that I decided I might as well make a blog post of it.

#Install Arch Linux
Install Arch Linux.
Getting a base system shouldn't be too hard, and there's guides available.
The only thing I recommend is that you set up your partitions _first_ if possible.
The partitioning from within the Arch install isn't very good.

If all has gone well, after logging into your new system, you should be staring and a black and white tty.
Login as root.
Which should be the only available option at this point.

#Setup pacman
Pacman is Arch's pacage manager -- similar to Debian/Ubuntu's apt, and OS X's homebrew.
It's most similar in design and philosophy to the BSD ports sytem, however.
To start,
```bash
    pacman-key --init
```
Mash keys to generate entropy.
That is to say, the process of generating a key goes faster if you provide a source of randomness to the computer.
```bash
    pacman-key --populate archlinux
```
Answer yes to everything, but hopefully that goes without saying.

Next, we're going to setup pacman's list of mirrors so that it only tries to download from the five fastest.
Big performance improvement.
```bash
    cd /etc/pacman.d
    cp mirrorlist mirrorlist.backup
    pacman -S reflector
    reflector -l 5 --sort rate --save /etc/pacman.d/mirrorlist
```
To update and upgrade everything, do the following:
```bash
    pacman -Syyu
```
Make sure to use the -yy flag instead of a single -y as usual when you've updated the mirrorlist.
That forces pacman to re-examine the mirror list even if it thinks it's up to date.

#Setup a user environment
Install Git and ZSH, then clone all your dotfiles into a new user's home directory.
```bash
    pacman -S git zsh vim
    git clone https://github.com/austinyun/dotfiles.git ~/home/austin
```
Then run `adduser` to make said user.
Make sure to add your new user to the wheel group, then run `visudo` and uncomment the line letting people in the wheel group use sudo commands.
Exit and log back in as said user now.

Next we'll make the `.xinitrc` file executable (has to be for some reason), and set our user's default shell to ZSH.
Obviously if you're username isn't austin, substitute YOUR username in here.
```bash
    chmod +x /home/austin/.xinitrc
    chsh -s $(which zsh) austin
```
Change the colors you see in the terminal when you run the `ls` command and the like with:
```bash
    eval `dircolors ~/.dircolors`
```
Now get all the vim plugin goodness working.
```bash
    git clone https://github.com/gmarik/vundle.git ~/.vim/bundle/vundle
    vim +BundleInstall +qall
```
I have my vim store backup and undo files in a central location, so you have to make those directories:
```bash
    mkdir -p ~/.vim/tmp/undo
    mkdir -p ~/.vim/tmp/backup
```

#Install GUI stuff
Video related stuff.
`xf86-video-nouveau` and `nouveau-dri` are Nvidia specific!
Check the [Arch Wiki](http://wiki.archlinux.org) for specifics on your video card.

You'll notice I chose `lilyterm` as my terminal emulator.
I really like it.
Really, really!
```bash
    pacman -S xorg-server xorg-utils xf86-input-mouse xf86-input-keyboard
    pacman -S xf86-video-nouveau nouveau-dri
    pacman -S slim lilyterm dina-font
```
The XMonad window manager and some tools to help with it.
This is going to take a minute since XMonad depends on the entire Haskell ecosystem, it seems.
```bash
    pacman -S xmonad xmonad-contrib xmobar dmenu cabal-install
```
Login manager, gVim (which will give you vanilla vim too), and a terminal emulator.
```bash
    pacman -S slim terminator
```
Then to get sound working, install `alsa-utils`, run `alsamixer`, select the master channel with the left and right arrow keys, hit `m` to unmute it, and press the up arrow key to raise the volume.

```bash
    pacman -S alsa-utils
    alsamixer
```
Install whatever other programs you want at this point with `pacman -S` and the name of the package.
I use Google Chrome as my browser, for instance, so:
```bash
    pacman -S chromium
```
Add `slim` and `dbus` in DAEMONS under `/etc/rc.conf` with your text editor of choice.

And now you can just use Google to search for other software you need.
Yay.

#Thunar (file manager)
```bash
    pacman -S thunar thunar-archive-plugin thunar-media-tags-plugin
    pacman -S tumbler gvfs polkit-gnome gtk-engines gtk-theme-switch2 feh
```
Run `gtk-theme-switch2` and switch to Clearlooks, ASAP.
The default GTK theme is unbearably ugly.
I've also included `feh` in there, which is an image viewer that lets you set desktop backgrounds.
Cool.

Congratulations, you now have a basic, but very pretty Arch Linux install with XMonad as the window manager and almost zero cruft.
