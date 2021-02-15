# coc-nvim-config
## setup my coc-nvim config

### Install nvim and plugins

1. install nvim (refer to nvim website)

```
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim.appimage
chmod u+x nvim.appimage
./nvim.appimage
```

2. install coc

follow https://github.com/neoclide/coc.nvim, install js and vim-plug:

```
curl -sL install-node.now.sh/lts | bash
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
 ```

3. Install all nvim plugins:

```
:PlugInstall
:PlugUpdate
```

### Download conternt of this repo to .config

```
mkdir -p ~/.config
cd ~/.config

### Fix slow startup issue (optional)

if nvim starts very slow, possibly because the nerdtree plugin is not working well. Remove all nerdtree related config in ~/config/nvim/init.vim and things should work

### Check health (optional)

open nvim, run `:checkhealth`, follow instructions to install additional dependencies if needed

git init
git remote add origin git@github.com:leinxx/coc-nvim-config.git
git pull origin master
```

### set fzf for file and content search:

1. install rpgrep for command `:Rg` to work:

```
$ curl -LO https://github.com/BurntSushi/ripgrep/releases/download/11.0.2/ripgrep_11.0.2_amd64.deb
$ sudo dpkg -i ripgrep_11.0.2_amd64.deb
```

