# Getting started with Fluent DOM

This is a small, step-by-step tutorial showing a simple way to get started with Fluent in a web project built from scratch using [Fluent.js](https://github.com/projectfluent/fluent.js/).

We will build up to localizing a `<h1>` element using the following syntax:

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
>     <h1 data-l10n-id='hello'>Localize me!</h1>
>   </body>
> </html>
> ```

The tutorial will show how to set up your localization resources for your desired locales, and how to retrieve values from those resources to localize content.

We will be using [Node Package Manager (npm)](https://www.npmjs.com/) and [Parcel](https://parceljs.org/) in this tutorial.