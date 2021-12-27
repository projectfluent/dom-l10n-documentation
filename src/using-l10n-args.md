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
