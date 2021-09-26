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


### set fzf for file and content search:

1. install rpgrep for command `:Rg` to work:

```
curl -LO https://github.com/BurntSushi/ripgrep/releases/download/11.0.2/ripgrep_11.0.2_amd64.deb
sudo dpkg -i ripgrep_11.0.2_amd64.deb
```

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

### Check health (optional)

open nvim, run `:checkhealth`, follow instructions to install additional dependencies if needed
