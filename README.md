# macOS Setup Guide

This guide covers the basics of setting up a friendly and productive coding environment on a new Mac :computer:

> Some configurations will be made using the recomendations in this [guide](https://github.com/drduh/macOS-Security-and-Privacy-Guide/blob/master/README.md).

## System Preferences

### Latest Update

The first thing you should do is update your system. To do that go:
**Apple menu () > About This Mac > Software Update.**

### Network

Open a Terminal and run the following commands:

```sh
# Changing the computer name
sudo scutil --set ComputerName GMacBook
sudo scutil --set LocalHostName GMacBook
# Generate a backup copy of default hosts file
sudo cp /etc/hosts /etc/hosts.default-backup
# Block known adware and malware domains
curl https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts | sudo tee -a /etc/hosts
# Disable Safari from opening a website if connect to a captive portal
 sudo defaults write /Library/Preferences/SystemConfiguration/com.apple.captive.control.plist Active -bool false
```

### Trackpad

- _Point & Click_
  - Enable _Tap to click with one finger_
  - Change _Secondary click_ to _Right corner_
  - Check _Three Finger Drag_
- _Scroll & Zoom_
  - Uncheck _all_ apart from _Zoom in and out_

### Dock

- _Visual Settings_
  - Remove _workspace auto-switching_ by running the following command:

```sh
defaults write com.apple.dock workspaces-auto-swoosh -bool NO
killall Dock # Restart the Dock process
```

### Finder

- General
  - Change _New finder window show_ to open in your _Home Directory_
- Sidebar
  - Add _Home_ and your _Developer Directory_
  - Uncheck all _Shared_ boxes

### Menubar

- Change _battery_ to _Show percentage symbols_

### Spotlight

- Uncheck _fonts_, _images_, _files_ etc.

### Accounts

- Add an _iCloud account_ and sync _Calendar_, _Find my Mac_, _Contacts_ etc.

### User Defaults

- Change the _default folder for screenshots_
  - Open the terminal and create the folder where you would like to store
    your screenshots: `mkdir -p /path/to/screenshots/`
  - Then run the following command: `defaults write com.apple.screencapture location /path/to/screenshots/ && killall SystemUIServer`

## Xcode

Xcode is an integrated development environment for a macOS containing a suite of software development tools developed by Apple for developing software for macOS, iOS, watchOS and tvOS.

For installing Xcode command line tools run:

```sh
sudo xcode-select --install
```

## Homebrew

_The missing package manager for macOS_ is an essential tool for any developer.

### Installation

To install Homebrew run the following in a terminal:

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

brew update && brew upgrade
```

## Homebrew Cask

Cask extends Homebrew and allows you to install large binary files via command-line tool.
You can for example install applications like Google Chrome, Dropbox, VLC and others.
No more downloading `.dmg` files and dragging to your Application folder!

To start using Homebrew Cask, you just need Homebrew installed and search applications with
the flag `--cask`.

### Quick Look Plugins

These plugins add support for the corresponding files type to Mac Quick Look (In Finder, mark a file
and press space to start a Quick Look). The plugins includes features like syntax highlighting, Markdown,
rendering, preview of JSON, patch files, CSV, ZIP files and more.

```sh
brew install --cask \
    qlcolorcode \
    qlstephen \
    qlmarkdown \
    quicklook-json \
    qlprettypatch \
    quicklook-csv \
    betterzip \
    webpquicklook \
    suspicious-package
```

## Main Developer Software

```sh
brew install git node n kubernetes-cli deno tree httpie htop bat kubectx kube-ps1
# Update latest version of npm
sudo npm i -g npm
# Define git name and email
git config --global user.name "Your Name"
git config --global user.email "Your Email"
```

## iTerm2

[iTerm2](https://iterm2.com) is an open source replacement for Apple's Terminal. It's highly customizable and comes with a lot of useful features.

### Installation

Use Homebrew to download and install:

```sh
brew install --cask iterm2
```

### Material Design

1. Download the file [`material-design-colors.itermcolors`](https://raw.githubusercontent.com/sagiomc/macos-setup/master/iterm2/material-design-colors.itermcolors)

2. _iTerm2 > Preferences > Profiles > Colors Tab_

3. Click _Color Presets..._

4. Click _Import..._

5. Select the `material-design-colors.itermcolors` file

6. Select the _material-design-colors_ from _Load Presets..._

### Minimal Theme

Choose minimal theme to have cleaner UI with smaller tabs by selecting:

_iTerm2 > Appearence > General > Theme > Minimal_

### Cascadia Font

I use the [Cascadia Font](https://github.com/microsoft/cascadia-code) from Microsoft in iTerm. To install, follow the next commands:

```sh
brew tap homebrew/cask-fonts

brew install --cask font-cascadia-code font-cascadia-code-pl font-cascadia-mono font-cascadia-mono-pl

```

After installing the font on your operating system you need to select it as a font in your iTerm profile.

_iTerm2 > Profiles > <your_profile> > Text > Font_

## Oh My Zsh

[Oh My Zsh](https://ohmyz.sh) is an open source, community-driven framework for managing your `zsh` configuration.
It comes with a bunch of features out of the box and improves your terminal experience.

### Installation

Run the following command

```sh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Install zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
# Install zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
# Install zsh-completions
  git clone https://github.com/zsh-users/zsh-completions ${ZSH_CUSTOM:=~/.oh-my-zsh/custom}/plugins/zsh-completions
```

### Customization

Download the file [`zshrc`](https://raw.githubusercontent.com/sagiomc/macos-setup/master/oh-my-zsh/zshrc)
and replace the default file in `~/.zshrc`.

# References

[Michael Hoffmann Blog](https://www.mokkapps.de/blog/boost-your-productivity-by-using-the-terminal-iterm-and-zsh)
