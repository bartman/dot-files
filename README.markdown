Setup
=====

Download: <code>git clone git://github.com/tomhoover/dotfiles.git ~/.dotfiles</code>

Your various ~/.dotfiles* directories can be tracked by a revision control system like git, and easily shared with multiple computers.  You can have more than one ~/.dotfiles* directory (i.e. .dotfiles, .dotfiles-private, etc).  You are then able to share one with others (i.e. .dotfiles), and keep the other private (i.e. .dotfiles-private).

  * ~/.dotfiles* contain files like 'bashrc' and directories like 'vim'
  * ~/.* are symlinks to files within the various ~/.dotfiles* directories

The first time the script is executed, it will automatically link ~/bin/dotfiles to ~/.dotfiles/dotfiles.

Running
=======

Getting help:

        # dotfiles help
        dotfiles - manages symlink files from ~/.dotfiles/* to ~/.*

        Syntax: dotfiles [ <command> ] [ <options> ]

        Commands:

                list                 - list all files in ~/.dotfiles
                status               - status of available files
                install [-v] [-f]    - installs symlinks

Checking on the status:

        # dotfiles status
        zshrc                         OK
        bashrc                        .
        vimrc                         file

'OK' means that there is a ~/.zshrc symlink to ~/.dotfiles/zshrc.  'file'
means that there is a ~/.zshrc file, but we could convert it into a
symlink.  A dot means that the ~/.bashrc is not populated.

You can install new symlinks:

        # dotfiles install
        installing .zshrc                         ... skipped, OK
        installing .bashrc
        installing .vimrc
        ln: creating symbolic link `/home/bart/.vimrc': File exists

The above skipped .zshrc, installed a symlink for .bashrc, stopped at
vimrc because there was a conflict.

Support for host-specific files
===============================

The easiest way to illustrate is with an example.  Let's say my ~/.dotfiles directory contains the following files:

  * bashrc
  * bashrc:ariel
  * profile
  * profile:bethel

If the hostname of my computer is ariel, the following links are created when executing <code>dotfiles install</code>:

  * .bashrc -> .dotfiles/bashrc:ariel
  * .profile -> .dotfiles/profile

If the hostname of my computer is bethel, the following links would be created instead:

  * .bashrc -> .dotfiles/bashrc
  * .profile -> .dotfiles/profile:bethel

And, finally, if the hostname of my computer is carmel, the following links would be created:

  * .bashrc -> .dotfiles/bashrc
  * .profile -> .dotfiles/profile

