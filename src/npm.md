# Installing NPM

To install [Node Package Manager (npm)](https://www.npmjs.com/), we will be using [Node Version Manager (nvm)](https://github.com/nvm-sh/nvm#installing-and-updating).

Please navigate to the NVM repository and follow the instructions for the [Install & Upate Script](https://github.com/nvm-sh/nvm#install--update-script) section.

Note that their examples pipe to `bash`. If you are using another shell, such as `zsh`, you will need to change this to match your desired shell.

After running their install script, you should be able to close and re-open your terminal, then type `nvm` to verify that it is installed.

```
nvm --version
```
> ```
> 0.38.0
> ```

Next, we will install `npm` via

```
nvm install node
```

And then we can verify that `npm` is installed via

```
npm --version
```
> ```
> 7.24.0
> ```

Next we will build a basic skeleton of a project for using Fluent DOM.