# Installing NPM

To install [Node Package Manager (npm)](https://www.npmjs.com/), we will be using [Node Version Manager (nvm)](https://github.com/nvm-sh/nvm#installing-and-updating).

Navigate to the NVM repository and follow the instructions for the [Install & Upate Script](https://github.com/nvm-sh/nvm#install--update-script) section.

Note that their examples pipe to `bash`. If you are using another shell, such as `zsh`, you will need to change this to match your desired shell.

After running their install script, you should be able to close and re-open your terminal and verify that it was installed correctly by checking the version.

```
nvm --version
```
> ```
> 0.38.0
> ```

Next, we will install `npm` through `nvm`.

```
nvm install node
```

Now we can verify that `npm` is installed.

```
npm --version
```
> ```
> 7.24.0
> ```

---

In the [next section](./project-setup.md) we will build a basic skeleton of a project for using Fluent DOM.