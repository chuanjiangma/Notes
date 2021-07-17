# Install and Setup Emacs and Doom-Emacs(MacOS)

[toc]

## Prerequisites

- brew
- git 2.23+
- emacs 27.1+
- [ripgrep](https://github.com/BurntSushi/ripgrep) 11.0+
- GNU `find`
- [fd](https://github.com/sharkdp/fd) 7.3.0+ 
- doom-emacs

## Installation

### Install brew

Refer to the manual from official website:

```bash
/bin/bash -c "$(curl -kfsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

> considering that we may fail when using `curl`  with ssl certification, we add `-k` to the command above.

### Install or update git

Use `brew` to install git:

```bash
brew install git
```

### Install emacs

Install emacs with brew. If the version of emacs does not satisfy the requisite, install emacs by source building referring to the official document and manual.

Simply install emacs with brew:

```bash
brew update && brew install emacs
```

### Install ripgrep

`ripgrep` is a line oriented search tool and perform great in emacs. We can install it through brew:

```bash
brew install ripgrep
```

### Install GNU find

```bash
brew install findutils
```

### Install fd

```bash
brew install fd
```

### Install doom-emacs

```bash
git clone --depth 1 https://github.com/hlissner/doom-emacs ~/.emacs.d
~/.emacs.d/bin/doom install
```

When we run `doom install`, we may fail because of the network. Recommand `proxychains` for command `doom install` to use local SOCK5 proxy. Please refer to [this](https://github.com/haad/proxychains) and re-run the above command like `proxychains4 doom install`

It is better to config git http.proxy to speed up GitHub accessing if you have setup some proxy local. For example we have setup SOCK5 proxy on our host, then we can config git proxy like:

```bash
git config http.proxy 'socks5://localhost:1080' --global
git config https.proxy 'socks5://localhost:1080' --global
```

## Configuration

[TODO]

## Reference

- [Installation of brew](https://docs.brew.sh/Installation)

- [Installation of ripgrep](https://github.com/BurntSushi/ripgrep#installation)
- [Installation of fd](https://github.com/sharkdp/fd#installation)

