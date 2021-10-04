# L10n Args

The `data-l10n-args` provides a way to supply arguments to your localized content.

To build on the `data-l10n-id` example of a welcome message, perhaps we want to be able to provide a name of the person we are welcoming. To do this, we will need to add a `data-l10n-args` tag in addition to the `data-l10n-id`.

```html
<p id='welcome'
  data-l10n-id='hello'
  data-l10n-args='{"name": "world"}'>
</p>
```

And in the Fluent file, we will be able to use the argument within our localized content:

```
# $name - The name of the person to welcome.
hello = Hello {$name}
```