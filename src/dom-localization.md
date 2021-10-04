# DOMLocalization

The `DOMLocalization` class is an extension of the [`Localization`](./localization.md) class and is responsible for fetching resources and formatting translations for DOM elements.

## Functionality

---

> Includes all the functionality from [`Localization`](./localization.md)

---

### `constructor(resourceIds, generateBundles)`
> Creates a new `DOMLocalization` object given a list of `resourceIDs` and a `generateBundles` function that returns a generator over `FluentBundles` when given a list of `resourceIDs`.
>
> The `generateBundles` function's generator behavior acts as a fallbacking strategy for the availability of fluent resources.
>
> When localizing content in the ideal scenario, the `generateBundles` function will only ever have to produce one bundle. This would mean that the first bundle had translations for every requested localization.
>
> If the current bundle in unable to produce a translation, then the generator's next bundle will be retrieved in an attempt to find a translation, and so on.

---

### `setAttributes(element, id, args)`
> Set the [`data-l10n-id`](./l10n-id.md) and [`data-l10n-args`](./l10n-args.md) attributes on a DOM `element`. `DOMLocalization` makes use of mutation observers to detect change to `data-l10n-*` attributes and translate elements asynchronously. `setAttributes` is a convenience method which allows to translate DOM elements declaratively.
>
> You should always prefer to use [`data-l10n-id`](./l10n-id.md) on elements (statically in HTML or dynamically via `setAttributes`) over manually retrieving translations with `format`.  The use of attributes ensures that the elements can be retranslated when the user changes their language preferences.
>
> ```JavaScript
> localization.setAttributes(
>   document.querySelector('#welcome'), 'hello', { who: 'world' }
> );
> ```
>
> This will set the following attributes on the `#welcome` element. The MutationObserver will pick up this change and will localize the element asynchronously.
>
> ```html
> <p id='welcome'
>   data-l10n-id='hello'
>   data-l10n-args='{"who": "world"}'>
> </p>
> ```

---

### `getAttributes(element)`
> Get the `data-l10n-*` attributes from a DOM `element`.
> ```JavaScript
> localization.setAttributes(
>   document.querySelector('#welcome'), 'hello', { who: 'world' }
> )
> localization.getAttributes(
>   document.querySelector('#welcome')
> );
> // -> { id: 'hello', args: { who: 'world' } }
> ```

---

### `connectRoot(root)`
> Add new `root` to the list of roots managed by this `DOMLocalization`.
>
> Additionally, if this `DOMLocalization` has an observer, start observing the new `root` in order to translate mutations in it.
>
> The new `root` may not overlap with an existing root.

---

### `disconnectRoot(root)`
> Remove `root` from the list of roots managed by this `DOMLocalization`.
>
> Additionally, if this `DOMLocalization` has an observer, stop observing
> `root`.
>
> Returns `true` if the root was the last one managed by this
> `DOMLocalization`.

---

### `translateRoots()`
> Translate all roots associated with this `DOMLocalization`.

___

### `translateFragment(fragment)`
> Translate a DOM element or fragment asynchronously using this
> `DOMLocalization` object.
>
> Manually trigger the translation (or re-translation) of a DOM fragment.
> Use the `data-l10n-id` and `data-l10n-args` attributes to mark up the DOM with information about which translations to use.
>
> Returns a `Promise` that gets resolved once the translation is complete.

___

### `translateElements(elements)`
> Translate a list of DOM elements asynchronously using this `DOMLocalization` object.
>
> Manually trigger the translation (or re-translation) of a list of elements. Use the `data-l10n-id` and `data-l10n-args` attributes to mark up the DOM with information about which translations to use.
>
> Returns a `Promise` that gets resolved once the translation is complete.