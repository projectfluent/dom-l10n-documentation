# Adding fluent files

This tutorial will walk you through getting Parcel to add Fluent (`.ftl`) files as assets to your project.

If you don't have a working Parcel project, please refer to the [previous section](./project-setup.md).

---

Now that we have a working Parcel setup, we need to add some fluent files. We will store the files in a directory called `static` in our project root. Within the `static` directory we will create `localization/{locale}/main.ftl`, where each `{locale}` will be a specific locale.

In this tutorial, we will only create paths for the `en-US` and `es-MX` locales.

```
mkdir -p static/localization/en-US
touch static/localization/en-US/main.ftl
mkdir static/localization/es-MX
touch static/localization/es-MX/main.ftl
```
> ```
> fluent-playground
> ├── src
> │  ├── index.html
> │  └── index.js
> ├── static
> │  └── localization
> │     ├── en-US
> │     │  └── main.ftl
> │     └── es-MX
> │        └── main.ftl
> ├── package-lock.json
> └── package.json
> ```

Then we will populate our `main.ftl` files with our localized message using `hello` as our `data-l10n-id`.

> **_static/localization/en-US/main.ftl_**
> ```
> hello = Hello!
> ```

> **_static/localization/es-MX/main.ftl_**
> ```
> hello = ¡Hola!
> ```

---

Next we will need to install a Parcel plugin to copy over our static files to our project directory, then verify that it is added to your `package.json`.

```
npm install parcel-reporter-static-files-copy
```
> ```json
> "dependencies": {
>   "parcel-bundler": "^1.12.5",
>   "parcel-reporter-static-files-copy": "^1.3.4"
> }
> ```

Finally, in order to enable the static file copy, we need to create a `.parcelrc` file and add a few lines to it.
```
touch .parcelrc
```
> **_.parcelrc_**
> ```
> {
>   "extends": ["@parcel/config-default"],
>   "reporters": ["...", "parcel-reporter-static-files-copy"]
> }
> ```

---

Now when we run `npm start`, Parcel should build our `dist` directory with our assets included.

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

In the [next section](using-fluent.md) we will cover how to use Fluent DOM from JavaScript to localize our message.
