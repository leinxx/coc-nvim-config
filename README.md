# coc-nvim-config
## setup my coc-nvim config

### Install nvim and plugins

1. install nvim (refer to nvim website)

```
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim.appimage
chmod u+x nvim.appimage
./nvim.appimage
```
2. Download conternt of this repo to .config

```
mkdir -p ~/.config
cd ~/.config

git init
git remote add origin git@github.com:leinxx/coc-nvim-config.git
git pull origin master
```

3. install coc

follow https://github.com/neoclide/coc.nvim, install js and vim-plug:

```
curl -sL install-node.now.sh/lts | bash
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
 ```

4. Install all nvim plugins:

```
neovim
:PlugInstall
:PlugUpdate
```

5. Install python3 support (optional)

```
python3 -m pip install --user --upgrade pynvim
```

Replace coc-python with coc-pyright (coc-python is discontinued which causes error messages in nvim)

```
nvim
:CocUninstall coc-python
:CocInstall coc-pyright
```

### set fzf for file and content search:

1. install rpgrep for command `:Rg` to work:

```
curl -LO https://github.com/BurntSushi/ripgrep/releases/download/11.0.2/ripgrep_11.0.2_amd64.deb
sudo dpkg -i ripgrep_11.0.2_amd64.deb
```

### Setup pylance for coc:
Default coc-pyright language server often give false alarm for names defined in libs. To get vscode-level languange server, use pylance, which uses pyright in the hood, but with extensite improvements. It is currently a vscode extension.
Check gist [coc-pylance](https://gist.github.com/leinxx/c53eea5377d26b6d385133c58003ac1f) to setup pylance language server in nvim.

### Fix slow startup issue (optional)

if nvim starts very slow, possibly because the nerdtree plugin is not working well. Remove all nerdtree related config in ~/config/nvim/init.vim and things should work

### Install ccls

follow: https://github.com/MaskRay/ccls/wiki/Build.

for ubuntu18.04:

```

git clone --depth=1 --recursive https://github.com/MaskRay/ccls
cd ccls
wget -c http://releases.llvm.org/8.0.0/clang+llvm-8.0.0-x86_64-linux-gnu-ubuntu-18.04.tar.xz
tar xf clang+llvm-8.0.0-x86_64-linux-gnu-ubuntu-18.04.tar.xz
cmake -H. -BRelease -DCMAKE_BUILD_TYPE=Release -DCMAKE_PREFIX_PATH=$PWD/clang+llvm-8.0.0-x86_64-linux-gnu-ubuntu-18.04
cmake --build Release
cd Release
sudo make install
```

for Ubuntu 20.4:

```
sudo apt-get install clang
sudo apt-get install libclang-10-dev
git clone --depth=1 --recursive https://github.com/MaskRay/ccls
cd ccls
cmake -H. -BRelease -DCMAKE_BUILD_TYPE=Release -DCMAKE_PREFIX_PATH=$PWD/clang+llvm-8.0.0-x86_64-linux-gnu-ubuntu-18.04
cmake --build Release
cd Release
sudo make install
```

### Customize vim

Jump to definition in vertical split by "gv":

Add the following commands to the end of file ```~/.vim/plugged/coc.nvim/plugin/coc.vim```:
```
nmap <silent> gd :call CocAction('jumpDefinition')<CR>
nmap <silent> gs :call CocAction('jumpDefinition', 'split')<CR>
nmap <silent> gv :call CocAction('jumpDefinition', 'vsplit')<CR>
```

Add the following lines to the end of file `~/.config/nvim/init.vim`
```
" open list of opened files
nnoremap <silent>gb :Buffers<CR>
" search files in 'git list'
nnoremap <silent>g[ :GFiles<CR>
" search files in 'git status'
nnoremap <silent>g] :GFiles?<CR>
```


### Check health (optional)

open nvim, run `:checkhealth`, follow instructions to install additional dependencies if needed


## use proxies

nvim plugin uses github to install and update plugins. To use proxies, it can be set in ~/.gitconfig. for example:
```
[http]
    sslverify = false
    proxy = http://username:password@proxy_url:port
  [user]
    email = you email
    name = your name
  [https]
    sslverify = false
    proxy = http://username:password@proxy_url:port
  [core]
    editor = vi
  [credential]
    helper = store
  [filter "lfs"]
    clean = git-lfs clean -- %f
    smudge = git-lfs smudge -- %f
    process = git-lfs filter-process
    required = true
```

coc.nvim uses `~/.config/nvim/coc-settings.json` to set proxy. An example coc-setting.json:
```
  {

  "languageserver": {
      "ccls": {
        "command": "ccls",
        "filetypes": ["c", "cpp", "objc", "objcpp"],
        "rootPatterns": [".ccls", "compile_commands.json", ".git/", ".hg/"],
        "initializationOptions": {
           "cache": {
             "directory": "/tmp/ccls"
           }
         }
      }
    },
    "http.proxy": "http://username:password@proxy_url:port",
    "http.proxyStrictSSL": false,
     "https.rejectUnauthorized": false,
     "https.proxy": "http://username:password@proxy_url:port",
     "python.jediEnabled": false,
    "python.pythonPath": "~/.config/coc/extensions/node_modules/coc-pyright/python_path",
    "pyright.inlayHints.functionReturnTypes": true,
    "pyright.inlayHints.variableTypes": false
  }
```

check coc-pyright's readme for the setup of `python.pythonPath`, `pyright.inlayHints.functionReturnTypes` and `pyright.inlayHints.variableTypes`.


