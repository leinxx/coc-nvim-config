# coc-nvim-config
## setup my coc-nvim config

### Download conternt of this repo to .config

```
mkdir -p ~/.config
cd ~/.config
git init
git remote add origin git@github.com:leinxx/coc-nvim.git
git pull origin master
```

### set fzf for file and content search:

1. install rpgrep for command `:Rg` to work:

```
$ curl -LO https://github.com/BurntSushi/ripgrep/releases/download/11.0.2/ripgrep_11.0.2_amd64.deb
$ sudo dpkg -i ripgrep_11.0.2_amd64.deb
```

### Install nvim and plugins

1. install nvim (refer to nvim website)
2. Install all nvim plugins:

```
:PlugInstall
:PlugUpdate
```
