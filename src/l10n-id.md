# L10n ID

The L10n ID is an identifier that you assign to a DOM element to be localized.

For example, a welcome message may have a regular `id` of `welcome` so that you can query for it in JavaScript code and a `data-l10n-id` of `hello`.

```html
<p id='welcome'
  data-l10n-id='hello'
</p>
```

You will likely have multiple Fluent (`.ftl`) files for different locales that specify localized content for the `hello` `data-l10n-id`.

For example, for the `en` locale you might have:
```
hello = Hello
```

And for the `es` locale you might have:
```
hello = Hola
```

The `data-l10n-id` is like a contract between the element and its localized content.

This means that if the localized content changes, then the `data-l10n-id` must also change. For example, if I want my `en` message to read `Hello there` instead of just `Hello`, I will also need to change the `data-l10n-id`.

```html
<p id='welcome'
  data-l10n-id='hello-there'
</p>
```

```
hello-there = Hello there
```