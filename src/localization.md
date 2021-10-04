# Localization

The `Localization` class is a central high-level API for using Fluent.

## Functionality

---

### `constructor(resourceIds, generateBundles)`
> Creates a new `Localization` object given a list of `resourceIDs` and a `generateBundles` function that returns a generator over `FluentBundles` when given a list of `resourceIDs`.
>
> The `generateBundles` function's generator behavior acts as a fallbacking strategy for the availability of fluent resources.
>
> When localizing content in the ideal scenario, the `generateBundles` function will only ever have to produce one bundle. This would mean that the first bundle had translations for every requested localization.
>
> If the current bundle in unable to produce a translation, then the generator's next bundle will be retrieved in an attempt to find a translation, and so on.

---

### `addResourceIds(resourceIds, eager = false)`
> Adds resource IDs to this localization object.
> Accepts a boolean for whether to eagerly apply the changes
> with a default value of `false`.

---

### `removeResourceIds(resourceIds)`
> Removes resource IDs from this localization object.
> This operation is never eager.

---

### `formatValues(keys)`
> Retrives translations corresponding to the passed keys.
> Keys must be `{id, args}` objects.
>
> If all `keys` have available translations within the current `FluentBundle`
> then no fallbacking will occur. If a translation is missing, the
> localization object will retrieve the next bundle from the `generateBundles` function and so on.
>
> ```JavaScript
> docL10n.formatValues([
>   {id: 'hello', args: { who: 'Mary' }},
>   {id: 'hello', args: { who: 'John' }},
>   {id: 'welcome'}
> ]).then(console.log)
> ```

---

### `formatValue(id, args)`
>> **_Note:_**
>>
>> _Use this sparingly for one-off messages which do not need to be retranslated when the user change their language preferences, e.g. in notifications._
>
> Retrieves the translation corresponding to the `id`.
>
> If passed, `args` is a simple hash object with a list of variables that will be interpolated in the value of the translation.
>
> Returns a promise resolving to the translation string.
>
> ```JavaScript
> docL10n.formatValue(
>   'hello', { who: 'world' }
> ).then(console.log);
> ```