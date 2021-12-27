# Using L10n ID

This section assumes that you have followed the tutorial up through the [Using FLuent](./using-fluent.md) section, and that you have a working HTML page that localizes the following content.
> **_src/index.html_**
> ```HTML
> <!DOCTYPE html>
> <html>
>   <head>
>     <meta charset='UTF-8' />
>     <meta name='defaultLanguage' content='es-MX' />
>     <meta name='availableLanguages' content='en-US, es-MX' />
>     <link name='localization' content='./localization/{locale}/main.ftl' />
>     <script type='module' src='index.js'></script>
>   </head>
>   <body>
>     <h1 id='welcome'>Localize me!</h1>
>   </body>
> </html>
> ```

---

In our current implementation we are using JavaScript to query for the `<h1>` element through its identifier (`id='welcome'`). Then we are using our `DOMLocalization` object to set this element's attributes to `hello` to match the `data-l10n-id` that is specified in our Fluent (`.ftl`) files.
> ```JavaScript
> const welcome = document.getElementById("welcome");
> ...
> l10n.setAttributes(welcome, "hello");
> ```

---

This works fine, but one of the nice things about using Fluent DOM is the abstraction around using `data-l10n-id` directly in your HTML. Our `DOMLocalization` object can automatically observe the document and localize the elements who have matching L10n IDs without having to manually query for them in JavaScript.

To make this change, we are going to remove the `id='welcome'` from our `<h1>` element in `index.html`, and add `data-l10n-id='hello'`.
> ```HTML
> <h1 id='welcome' data-l10n-id='hello'>Localize me!</h1>
> ```


Then we are going to remove the lines in JavaScript that manually query for and modify the `<h1>` element.
> **_remove commented lines_**
> ```JavaScript
> //const welcome = document.getElementById("welcome");
> //console.log(welcome);
> //
> const resources = document.querySelector("link[name=localization]");
> const resourcePathTemplate = resources.attributes.content.nodeValue;
> console.log(resourcePathTemplate);
>
> const l10n = new DOMLocalization([resourcePathTemplate], generateBundles);
> l10n.connectRoot(document.documentElement);
> //l10n.setAttributes(welcome, "hello");
> l10n.translateRoots();
> ```

---

In this case, we fetch our resources, create our `DOMLocalization` object, connect it to the document, and then invoke `translateRoots()`. The `DOMLocalization` object will automatically see that our `<h1>` element has a `data-l10n-id='hello'`, which matches the ID in our Fluent (`.ftl`) files, and make the appropriate translation.

---

In the [next section](./using-l10n-args.md) we will cover how to pass arguments to our localized content using `data-l10n-args`.
