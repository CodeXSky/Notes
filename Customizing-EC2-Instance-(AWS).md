* The package manager for the EC2 instances is called `yum`.
* Make sure `wget` and `git` are installed. To install any of them type `sudo yum install git`.
* To install the [zsh shell](https://github.com/robbyrussell/oh-my-zsh) do `sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"`.
* To customize the zsh theme edit the `~/.zshrc` file and change the line where it says `ZSH_THEME="robbyrussell"`.
* Personally, I like the "example" theme, and I add these lines at the end:
**`# Other added by JFS
**export CLICOLOR=1
**export LSCOLORS=GxFxCxDxBxegedabagaced`