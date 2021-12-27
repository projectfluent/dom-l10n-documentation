# L10n Args

`data-l10n-args` provides a way to supply arguments to your localized content.

To build upon the `data-l10n-id` example of a welcome message, perhaps we want to be able to provide a name of the person we are welcoming. To do this, we will need to add a `data-l10n-args` tag in addition to the `data-l10n-id`.

```html
<p id='welcome'
  data-l10n-id='hello'
  data-l10n-args='{"name": "world"}'>
</p>
```

And in the Fluent file, we will be able to use the argument within our localized content:

```
# $name - The name of the person to welcome.
hello = Hello { $name }
```

In the example above, passing in `data-l10n-args='{"name:" "world"}'` would result in the final translation of `Hello world`.

---

## Limitations

At this time, Fluent DOM is only able to accept numbers and strings as `data-l10n-args`. It technically also supports dates, since dates can be represented as a number, however there is an open bug ([Bug1611754](https://bugzilla.mozilla.org/show_bug.cgi?id=1611754)) to support dates in a more straightforward way.
