Install Arch Linux
==================
Install Arch Linux. Getting a base system shouldn't be too hard, and there's
guides available. The only thing I recommend is that you set up your partitions
_first_ if possible. The partitioning from within the Arch install isn't very
good.

If all has gone well, after logging into your new system, you should be staring
and a black and white tty. Login as root. Which should be the only available
option at this point.

Setup pacman
============
Pacman is Arch's pacage manager -- similar to Debian/Ubuntu's apt, and OS X's
homebrew. It's most similar in design and philosophy to the BSD ports sytem,
however. To start,

    {% highlight bash %}pacman-key --init {% endhighlight %}

Mash keys to generate entropy. That is to say, the process of generating a key
goes faster if you provide a source of randomness to the computer.

    {% highlight bash %}pacman-key --populate archlinux{% endhighlight %}

Answer yes to everything, but hopefully that goes without saying.

Next, we're going to setup pacman's list of mirrors so that it only tries to
download from the six fastest. Big performance improvement.

    {% highlight bash %}cd /etc/pacman.d

    cp mirrorlist mirrorlist.backup
    rankmirrors -n 6 mirrorlist.backup > mirrorlist{% endhighlight %}

To update and upgrade everything, do the following:

    {% highlight bash %}pacman -Syyu{% endhighlight %}

Make sure to use the -yy flag instead of a single -y as usual when you've
updated the mirrorlist. That forces pacman to re-examine the mirror list even if
it thinks it's up to date.

Install Helpful Programs
========================
Login manager and terminal

    {% highlight bash %}pacman -S slim rxvt-unicode{% endhighlight %}

Git and the two best text editors, along with a graphical notepad replacement.

    {% highlight bash %}pacman -S git emacs gvim leafpad{% endhighlight %}

Video related stuff. xf86-video-nouveau and nouveau-dri are Nvidia specific!

    {% highlight bash %}pacman -S xorg-utils xf86-input-mouse xf86-input-keyboard xf86-video-nouveau nouveau-dri{% endhighlight %}

The XMonad window manager and some tools to help with it. This is going to take
a minute since XMonad depends on the entire Haskell ecosystem, it seems.

    {% highlight bash %}pacman -S xmonad xmonad-contrib xmobar trayer dmenu cabal-install{% endhighlight %}

Install whatever other programs you want at this point with pacman -S and the
name of the package. I use Google Chrome as my browser, for instance, so:

    {% highlight bash %}pacman -S chromium{% endhighlight %}

And now you can just use Google to search for other software you need. Yay.

Thunar (file manager)
=====================
    {% highlight bash %}pacman -S thunar thunar-archive-plugin thunar-media-tags-plugin tumbler gvfs polkit-gnome gtk-engines gtk-theme-switch2 feh{% endhighlight %}

Run gtk-theme-switch2 and switch to Clearlooks, ASAP. The default GTK theme is
unbearably ugly. I've also included 'feh' in there, which is an image viewer
that lets you set desktop backgrounds. Cool.

Setting up Git
==============
First, we need to set up authentication. Open ~/.ssh/id\_rsa.pub and copy it to
your github account. Log in to github, click "edit your profile", click "SSH
Keys" on the left, and paste the contents of the file in there.

Configuration
=============
Run the 'adduser' command to make a new user so you're not logged in as root all
the time. Make sure to add your new user to the wheel group.

Then run 'visudo' and uncomment the line letting people in the wheel group use
sudo commands.

Add slim and dbus in DAEMONS under /etc/rc.conf with your text editor of choice.

Now, use git to clone my dotfiles repo into your home folder, and grab the font
I use for my terminal, vim, etc.

    {% highlight bash %}git clone git@github.com:austinyun/dotfiles.git ~/
    sudo pacman -S dina-font
    cd .xmonad && xmonad --recompile{% endhighlight %}

Log out, and log back in to your XMonad and things should be different. Your
terminal should now be prettier, but let's make it even prettier by fixing the
colors you get when you run the ls or dir commands.

    {% highlight bash %}eval `dircolors ~/.dircolors.ansi-dark`{% endhighlight %}

Now get all the vim plugin goodness working.

    {% highlight bash %}git clone git@github.com:gmarik/vundle.git ~/.vim/bundle/vundle
    vim +BundleInstall +qall{% endhighlight %}

Congratulations, you now have a basic, but very pretty Arch Linux install with
XMonad as the window manager and almost zero cruft.
