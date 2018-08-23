### Working with Virtual Environments
#### Installation
* I have installed `virtualenv` through `pip3 install virtualenv`
* Additionally, I installed `virtualenvwrapper` with:
  * `pip3 install virtualenvwrapper`
  * `export WORKON_HOME=~/Envs`
  * Note, I had to change the path to python to be able to use Hombrew's python3: `export VIRTUALENVWRAPPER_PYTHON=/usr/local/bin/python3`
  * `source /usr/local/bin/virtualenvwrapper.sh`
  * I added these last three lines to my `.zshrc` file so that the paths are recognized.

#### Usage
* Create a virtual environment: `mkvirtualenv venv`
* Work on a virtual environment (activate): `workon venv`
* Deactivate a virtual environment: `deactivate`
* Remove a virtual environment: `rmvirtualenv venv`
* List all virtual environments: `lsvirtualenv`

#### More
* Most of this information comes from [The Hitchhikers Guide to Python](https://python-guide-ru.readthedocs.io/en/latest/dev/virtualenvs.html)
