# Install different perl versions with plenv under babun/cygwin

babun : http://babun.github.io/

plenv : https://github.com/tokuhirom/plenv

- 0 - see TROUBLESHOOTING sections (7 and 8) if needed
- 1 - Launch [babun] (http://babun.github.io/) (ie `zsh` shell)
- 2 - Check or install packages with `pact`
```sh
pact install patch
pact install git
pact install make
pact install gcc-core
pact install zlib-devel
pact install gcc-g++
pact install curl
pact install autoconf
pact install libiconv
pact install libiconv-devel
pact install libcrypt0
```
- 3 - Install [plenv] (https://github.com/tokuhirom/plenv)
```sh
git clone http://github.com/tokuhirom/plenv.git ~/.plenv
```
- 4 - PATH
```sh
echo 'export PATH="$HOME/.plenv/bin:$PATH"' >> ~/.zshrc
```
- 5 - Install plenv (last steps) 
```sh
echo 'eval "$(plenv init - zsh)"' >> ~/.zshrc                    
exec $SHELL -l
git clone http://github.com/tokuhirom/Perl-Build.git ~/.plenv/plugins/perl-build/
```
- 6 - That's it, you can now use `plenv` to install new perl version
   example :  
```sh
plenv install -l
plenv install 5.24.0
plenv rehash
plenv versions
plenv global 5.24.0
PLENV_INSTALL_CPANM="-v" plenv install-cpanm
perl -v
```
- 7 - TROUBLESHOOTING - Fix the mix of versions of `g++` and `cyglto_plugin.dll`  
   See more information about this issue on [stackoverflow](http://stackoverflow.com/questions/19672892/cygwin-64-g-fuse-linker-plugin-error)
    
   Check versions with `g++ --version` and  `find /usr/lib/gcc -name cyglto_plugin.dll`. If there is a mix, try :  
```sh
pact update gcc-core
```
- 8 - TROUBLESHOOTING - Parens in PATH environment variable (this part is now useless for me)  
   Edit your `.zshrc` if you have PATH issue with `plenv install...` or other tools.  
   If `$PATH` variable contains foldernames with parens, perl installation could fail (5.14.2 for exemple). You can modify PATH and escape parens.  
   In `~/.zshrc` change `export PATH="$HOME/.plenv/bin:$PATH"` by :  
```sh
export PATH="$HOME/.plenv/bin:$(/usr/bin/echo $PATH | /usr/bin/sed -e 's/\([()]\)/\\\1/g')"
```
   Don't forget that dirty thing and edit your `.zshrc` if you have PATH issue with `plenv install...` or other tools.

