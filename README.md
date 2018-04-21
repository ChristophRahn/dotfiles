# crahn does dotfiles - forked from jldeens's repo

## WSL specifics

The configure script in this repo sets up your entire system from scratch.
Since the current shell for WSL has some issues with scripts running in the tmux status bar, I highly recommend to use the [emulator from goreliu](https://github.com/goreliu/wsl-terminal).

### WSL Configuration / Install
Run the following to configure WSL from scratch...
```sh
bash -c "$(curl -fsSL https://raw.githubusercontent.com/ChristophRahn/dotfiles/master/configure.sh)"
```
### WSL Emulator Install and Setup
Run the following command from an Administrator PowerShell prompt...
```powershell
Set-ExecutionPolicy Bypass; irm 'https://raw.githubusercontent.com/ChristophRahn/dotfiles/master/wslterm.ps1' | iex;
```

For zsh to start as the default shell, we need to change the base configuration for the emulator. To fix this, you will find a wsl-terminal.conf file in the /mnt/c/Users/[UserProfile]/wsl-terminal/etc directory. You need to comment out line 4 and uncomment line 6, as [Jessica explained in her blog](http://jessicadeen.com/tech/badass-terminal-wsl-macos-and-ubuntu-dotfiles-update/).
You also want to select a theme for the emulator, *base16-solarized-dark.minttyrc* is highly recommended. Finally we have to install a font that supports all the unicode characters used in this shell theme.
There are two fonts available in this repository, pick your favorite. From my experience, the *Source Code Pro Nerd Font* seems to play nicely with higher DPI monitors like the Dell 2716DG 1440p one I use at home.

## Notes
Your dotfiles are how you personalize your system. These are mine.

I was a little tired of having long alias files and everything strewn about
(which is extremely common on other dotfiles projects, too). That led to this
project being much more topic-centric. I realized I could split a lot of things
up into the main areas I used (git, system libraries, and so on), so I
structured the project accordingly.

If you're interested in the philosophy behind why projects like these are
awesome, you might want to [read Holman's post on the
subject](http://zachholman.com/2010/08/dotfiles-are-meant-to-be-forked/).

## Topical

Everything's built around topic areas. If you're adding a new area to your
forked dotfiles — say, "Java" — you can simply add a `java` directory and put
files in there. Anything with an extension of `.zsh` will get automatically
included into your shell. Anything with an extension of `.symlink` will get
symlinked without extension into `$HOME` when you run `script/bootstrap`.

## What's inside

A lot of stuff. Seriously, a lot of stuff. Check them out in the file browser
above and see what components may mesh up with you.
[Fork holman's](https://github.com/holman/dotfiles/fork) or [Fork jessica's](htps://github.com/jldeen/dotfiles/fork) or [Fork mine](htps://github.com/ChristophRahn/dotfiles/fork), remove what you don't
use, and build on what you do use.

## Components

There's a few special files in the hierarchy.

- **bin/**: Anything in `bin/` will get added to your `$PATH` and be made
  available everywhere.
- **Brewfile**: This is a list of applications for [Homebrew Cask](https://caskroom.github.io) to install: things like Chrome and 1Password and Adium and stuff. Might want to edit this file before running any initial setup.
- **topic/\*.zsh**: Any files ending in `.zsh` get loaded into your
  environment.
- **topic/path.zsh**: Any file named `path.zsh` is loaded first and is
  expected to setup `$PATH` or similar.
- **topic/completion.zsh**: Any file named `completion.zsh` is loaded
  last and is expected to setup autocomplete.
- **topic/install.sh**: Any file named `install.sh` is executed when you run `script/install`. To avoid being loaded automatically, its extension is `.sh`, not `.zsh`.
- **topic/\*.symlink**: Any file ending in `*.symlink` gets symlinked into
  your `$HOME`. This is so you can keep all of those versioned in your dotfiles
  but still keep those autoloaded files in your home directory. These get
  symlinked in when you run `script/bootstrap`.

## Git clone

If you wish to clone these filesa and run scripts manually, run this:

```sh
git clone https://github.com/ChristophRahn/dotfiles.git ~/.dotfiles
cd ~/.dotfiles
script/bootstrap
```

This will symlink the appropriate files in `.dotfiles` to your home directory.
Everything is configured and tweaked within `~/.dotfiles`.

The main file you'll want to change right off the bat is `zsh/zshrc.symlink`,
which sets up a few paths that'll be different on your particular machine. You also might want to configure `.tmux.conf` since I run a few scripts in the status bar.

`dot` is a simple script that installs some dependencies, sets sane macOS
defaults, and so on. Tweak this script, and occasionally run `dot` from
time to time to keep your environment fresh and up-to-date. You can find
this script in `bin/`.

## Bugs

I want this to work for everyone; that means when you clone it down it should
work for you even though you may not have `rbenv` installed, for example. That
said, I do use this as *my* dotfiles, so there's a good chance I may break
something if I forget to make a check for a dependency.

If you're brand-new to the project and run into any blockers, please
[open an issue](https://github.com/ChristophRahn/dotfiles/issues) on this repository
and I'd love to get it fixed for you!

## Thanks

Thanks to Jessica for providing dotfiles that work across Linux, Mac and WSL!
