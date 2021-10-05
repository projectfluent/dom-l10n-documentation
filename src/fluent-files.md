# Adding fluent files

This tutorial will walk you through getting Parcel to add Fluent (`.ftl`) files as assets to your project.

If you don't have a working Parcel project, please refer to the [previous section](./project-setup.md).

---

Now that we have a working Parcel setup, we need to add some fluent files. We will store the files in `src`, under an `assets`. Within `assets` we will have `localization/{locale}/main.ftl`.

In this tutorial, we will only create files for the `en-US` and `es-MX` locales.

```
mkdir -p src/assets/localization/en-US
touch src/assets/localization/en-US/main.ftl
mkdir src/assets/localization/es-MX
touch src/assets/localization/es-MX/main.ftl
```
> ```
> fluent-playground
> ├── src
> │  ├── assets
> │  │  └── localization
> │  │     ├── en-US
> │  │     │  └── main.ftl
> │  │     └── es-MX
> │  │        └── main.ftl
> │  ├── index.html
> │  └── index.js
> └── package.json
> ```

Then we will populate our `main.ftl` files with our localzed message using `hello` as our `data-l10n-id`.

> **_src/assets/localization/en-US/main.ftl_**
> ```
> hello = Hello!
> ```

> **_src/assets/localization/es-MX/main.ftl_**
> ```
> hello = ¡Hola!
> ```

---

Next we will need to install a Parcel plugin to copy over our assets to our project directory and verify that it is added to your `package.json`.

```
npm install parcel-plugin-asset-copier
```
> ```json
> "dependencies": {
>   "parcel-bundler": "^1.12.5",
>   "parcel-plugin-asset-copier": "^1.1.0"
> }
> ```

Finally, we need to add the path to our assets to the `package.json` by including the following line:

```json
"assetsPath": "./src/assets",
```

---

Now, when we run `npm start`, Parcel should build our `dist` directory with our assets included.

```
.
├── dist
│  ├── localization
│  │  ├── en-US
│  │  │  └── main.ftl
│  │  └── es-MX
│  │     └── main.ftl
│  ├── index.html
│  ├── src.e31bb0bc.js
│  └── src.e31bb0bc.js.map
...
```

---

In the next section we will cover how to use Fluent DOM from JavaScript to localize our message.