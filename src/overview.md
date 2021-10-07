# Overview

[Fluent](https://projectfluent.org/) is a family of localization specifications, implementations and good practices developed by Mozilla.

This documentation is intended to be a starting point for anyone looking to understand and learn to use Fluent DOM, which is a set of abstractions that allow for localizing content in HTML pages as they relate to the [Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction) (DOM).

---

## Example

We can specify translations in Fluent (`.ftl`) files for different languages. Here we specify translations for `en-US` and `es-MX`.

> **_en-US/main.ftl_**
> ```
> hello = Hello { $name }.
> ```

> **_es-MX/main.ftl_**
> ```
> hello = Hola { $name }.
> ```

---

We can then use our Fluent translations to localize the content of elements in the HTML. In this example `<h1>` element will be translated by Fluent to say `"Hola Erik."`, because we specify the `defaultLanguage` to be `es-MX`, which matches our translation above.

> **_index.html_**
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
>     <h1 data-l10n-id='hello' data-l10n-args='{ "name": "Erik" }'>Hi!</h1>
>   </body>
> </html>
> ```

---

The following sectctions will explain the concepts behind Fluent DOM as well as present a walkthrough tutorial on how to set up a project from scratch that uses Fluent DOM to localize HTML content.