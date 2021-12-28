# Using L10n Args

This section assumes that you have followed the tutorial up through the [Using L10n ID](./using-l10n-id.md) 
section, and that you have a working HTML page that localizes the following content.
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
>     <h1 id='welcome' data-l10n-id='hello'>Localize me!</h1>
>   </body>
> </html>
> ```

---

We are now going to allow our localized welcome message to take in a variable as an argument.

In each of the two fluent files, we are going to add a comment describing the variable
in addition to adding the variable into our localized messages.

> **_static/localization/en-US/main.ftl_**
> ```
> # Variables:
> #  $name (String): the name of the person to greet.
> hello = Hello { $name }!
> ```

> **_static/localization/en-US/main.ftl_**
> ```
> # Variables:
> #  $name (String): the name of the person to greet.
> hello = ¡Hola { $name }!
> ```

---

Now, when we run the program, we will still see our localized message for our locale, but since
Fluent doesn't have any default value for this variable, it will just passthrough the variable name.

```
¡Hola ⁨{$name}⁩!
```

This is intended behavior if Fluent is unable to find any values to match the variable for this message.

To fix this, we can add a default value in the HTML via the `data-l10n-args` attribute:

> **_src/index.html_**
> ```HTML
> <h1 id='welcome' data-l10n-id='hello' data-l10n-args='{"name": "world"}'>Localize me!</h1>
> ```

Now, when our DOMLocalization is translating this element, it will see the default argument for `$name`
and provide the value `"world"` to the localized message.

When we run the program again, we should now see:

```
¡Hola ⁨world⁩!
```
---

We can also pass in a new variable to the localized message via JavaScript.


To pass in a new variable we will call the `setAttributes()` function to pass in a new argument
to the element before we call `translateRoots()`.

> **_src/index.js_**
>
> ```JavaScript
> const element = document.getElementById('welcome');
> l10n.setAttributes(
>   element, 'hello', { name: 'Erik' }
> );
> l10n.translateRoots();
> ```

Now, when we run the program, we should see that our element was localized with the new, non-default argument.

```
¡Hola ⁨Erik⁩!
```
---

Congratulations! You are now localizing an HTML page utilizing Fluent DOM with `data-l10n-id` and `data-l10n-args`.
