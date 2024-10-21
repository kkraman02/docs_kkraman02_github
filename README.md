
### Getting started

1. Install dependencies:

```
$ git clone https://github.com/kkraman02/docs_kkraman02_github.git
$ cd docs_kkraman02_github
$ npm install
$ mkdir ~/.npm-global
$ npm config set prefix '~/.npm-global'
$ export PATH=~/.npm-global/bin:$PATH
$ source ~/.bashrc
$ npm install hexo-cli -g
$ npm install hexo-tag-bootstrap 
$ npm install hexo-butterfly-tag-plugins-plus
```

__Note__: If you encounter a permissions error, do not attempt to use `sudo`. Instead, follow the instructions [here](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally#manually-change-npms-default-directory)

2. Generate HTML website:

```
$ hexo clean
$ hexo g
```

3. Run server on local side:

```
$ hexo s
