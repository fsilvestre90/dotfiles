# My dotfiles.

Works on *nix, optimized for OS X.

Managed using [Stow](http://www.gnu.org/software/stow/), so you can pick and
choose which programs to install.

This dotfile package is mainly influenced from [Jeff Widman's dotfiles](https://github.com/jeffwidman/dotfiles) with some other workflows I find useful.

If you have an application that could be configured using dotfiles, add it to this repository! I learned about iterm2 or zsh later in my development years and it significantly improved my workflow.

---
## Install steps on a clean OSX machine:

1. Make hidden files/folder [visible in Finder](http://apple.stackexchange.com/questions/99213/is-it-possible-to-always-show-hidden-dotfiles-in-open-save-dialogs):
      `defaults write -g AppleShowAllFiles -bool true`

2. Install desired binaries using your favorite package manager:
  - If on OSX, use Homebrew:
    1. Install [Homebrew](http://brew.sh/).
    2. Install [Homebrew Bundle](https://github.com/Homebrew/homebrew-bundle): `$ brew tap Homebrew/bundle`
    3. `$ brew bundle --file=~/.dotfiles/homebrew/.Brewfile`
    After the `.Brewfile` is symlinked into ``~/.Brewfile`, just use `$ brew bundle --global`.
  - Make sure Stow gets installed, we'll use this later to symlink the dotfiles.

4. Make ZSH the default shell:
  1. `$ sudo vim /etc/shells`
  2. Append the path to zsh - Homebrew sticks it in `/usr/local/bin/zsh`
  3. Save and exit
  4. `$ chsh -s /usr/local/bin/zsh`

5. Install Prezto:
  - Install [Jeff Widmans prezto config](https://github.com/jeffwidman/prezto) because it includes
  a plugin for [Atom](http://atom.io).

  `git clone --recursive git@github.com:jeffwidman/prezto.git "${ZDOTDIR:-$HOME}/.zprezto"`

  - The default Prezto instructions say to symlink the default config files.
    **Don't do this**; instead use Stow to symlink your own config files (instructions below).
  - To update Prezto: `git pull && git submodule update --init --recursive`

5. Now use `stow` to symlink the various config files:
  - `$ cd ~/.dotfiles/`
  - `$ stow PACKAGE_NAME` will symlink all the files inside of the package_name's folder into the parent directory (in this case, the user's home folder.)
  - Stow thoughtfully raises an error if the symlink destination already exists. For example, installing ZSH creates a default `~/.zshrc` and `~/.zshlogin`. Just delete these default files before stowing your customized versions.
  - If using a different OS than OS X, some packages may store their config files at a different location. For example, the fonts folder. Just specify the full destination path for Stow.
  - More info:
     - http://brandon.invergo.net/news/2012-05-26-using-gnu-stow-to-manage-your-dotfiles.html
     - http://taihen.org/managing-dotfiles-with-gnu-stow/
     - http://kianmeng.org/blog/2014/03/08/using-gnu-stow-to-manage-your-dotfiles/
  - Several config files aren't `stow`able--review the list below

6. ZSH completion scripts:
  Symlink any completion scripts into ``/usr/local/share/zsh/site-functions/``.
  The filename must begin with an `_` or `zsh` will not read it. Prezto caches
  the output of `compinit`, to rebuild the cache do: `rm -rf ~/.zcomp* && compinit`

  Note: Many homebrew formula automatically handle installing the formula's
  completion scripts. For example, `brew install the_silver_searcher`(`ag`)
  will also install a completion script for `ag` in `/usr/local/share/zsh/site-functions/`.

---
##List of config files

 - Atom - Settings are stowable, but packages purposefully excluded. Use `$ apm stars --install` to install all packages I've [starred](https://atom.io/users/jeffwidman/stars) on [atom.io/packages](https://atom.io/packages).
 - bash
 - git
 - Homebrew Brewfile - stowable, `brew bundle --global` will use $HOME/.Brewfile
 - tmux - #TODO
 - vim
 - zsh - includes prezto config files


---
##Misc Notes:

Place your ssh and pem files inside the `ssh` folder. You can edit the config file inside (review config_template for examples) to quickly ssh into frequently used machines.

After using stow for the `init` folder, run `~/.osx` to update your mac osx settings. *warning* Read through the file to verify these settings match your needs.

---
##TODO:

 - add ipython (replaces python interpreter)

---
## Thanks
 - [@jeffwidman]( https://github.com/jeffwidman/dotfiles) - Initial inspiration, great setup
 - [@sorin-ionescu](https://github.com/sorin-ionescu/prezto) - for prezto
 - [@mathiasbyens](https://github.com/mathiasbynens/dotfiles) - for his osx customization script
