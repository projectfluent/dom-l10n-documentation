# L10n ID

The L10n ID is an identifier that you assign to a DOM element to be localized.

For example, a welcome message may have a regular `id` of `welcome` and a `data-l10n-id` of `hello`. The regular `id` behaves as normal, a way to query for this element, such as with `getElementById()`. The `data-l10n-id` is intended to match a Fluent translation that will be used to localize this element.

```html
<p id='welcome' data-l10n-id='hello'></p>
```

We define our L10n IDs in Fluent (`.ftl`) files for each locale that we want to provide a translation. In the example above, the `data-l10n-id` is `hello`, so in the Fluent files we would define translations for the `hello` L10n ID.

For the `en` locale you might have:
> **_en/main.ftl_**
> ```
> hello = Hello
> ```

And for the `es` locale you might have:
> **_es/main.ftl_**
> ```
> hello = Hola
> ```

The `data-l10n-id` is like a social contract between the element and its localized content translation. Each ID is unique to a single translation. If translated content needs to be updated, then a new `data-l10n-id` must be provided. For example, if we want to change our `en` message from "Hello" to "Hello there," we need to replace the previous L10n ID `hello` with a new one, such as `hello-there`.

This new ID and content would then require a re-translation in every other locale, such as `es` in the example above. Additionally, HTML elements will need to use this new ID as well.

> **_en/main.ftl_**
> ```
> hello-there = Hello there
> ```

This new ID and content would then need to get re-translated for every other locale, such as `es` in the example above, and the HTML elements will also need to receive the new ID as well.

> **_index.html_**
> ```html
> <p id='welcome' data-l10n-id='hello-there'></p>
> ```
