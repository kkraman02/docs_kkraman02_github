
### Getting started on Ubuntu

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

### Getting started on macOS

1. Install Homebrew (if not already installed)

```bash
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

2. Install Git
```bash
$ brew install git
```

3. Clone repository
```bash
$ git clone https://github.com/kkraman02/docs_kkraman02_github.git
$ cd docs_kkraman02_github
```

4. Install node version manager(NVM)
```bash
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
```

5. Load NVM into current
```bash
$ export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
```
To auto-load nvm for new sessions, add the above lines to your shell profile (~/.zshrc or ~/.bash_profile, depending on your shell).

- For zsh users:
```bash
$ nano ~/.zshrc
```

- For bash users:
```bash
$ nano ~/.bash_profile
```

Paste the lines, save the file (Ctrl+O, Enter, Ctrl+X), then reload your shell:
```bash
$ source ~/.zshrc   # for zsh users
$ source ~/.bash_profile   # for bash users
```

6. Install Node.js(v18)
```bash
$ nvm install 18
$ nvm use 18
$ nvm alias default 18
```

7. Cofigure NPM global directory
```bash
$ mkdir ~/.npm-global
$ npm config set prefix '~/.npm-global'
```
Add npm global directory to your path permanently by adding this line to your profile file (~/.zshrc or ~/.bash_profile):
```bash
$ export PATH=~/.npm-global/bin:$PATH
```
Then reload your shell:
```bash
$ source ~/.zshrc   # for zsh users
$ source ~/.bash_profile   # for bash users
```

8. Install Hexo and plugins
```bash
$ npm install hexo-cli -g
$ npm install hexo-tag-bootstrap
$ npm install hexo-butterfly-tag-plugins-plus
```
9. Generate and preview your website
```bash
$ hexo clean
$ hexo g
$ hexo s
```
You can directly copy this markdown into your project or documentation!
