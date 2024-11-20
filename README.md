
### Getting started

1. Install dependencies:

```sh
$ git clone https://github.com/kkraman02/docs_kkraman02_github.git
$ cd docs_kkraman02_github
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
$ source ~/.nvm/nvm.sh
$ nvm install 18
$ nvm use 18
$ nvm use --delete-prefix v18.20.5 --silent
$ mkdir ~/.npm-global
$ npm config set prefix '~/.npm-global'
$ export PATH=~/.npm-global/bin:$PATH
```
```sh
$ sudo nano ~/.bashrc
$ export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" # This loads nvm bash_completion
$ nvm alias default 18
$ source ~/.bashrc
$ npm install hexo-cli -g
$ npm install hexo-tag-bootstrap 
$ npm install hexo-butterfly-tag-plugins-plus
```

__Note__: If you encounter a permissions error, do not attempt to use `sudo`. Instead, follow the instructions [here](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally#manually-change-npms-default-directory)

2. Generate HTML website:

```sh
$ hexo clean
$ hexo g
```

3. Run server on local side:

```sh
$ hexo s
```
