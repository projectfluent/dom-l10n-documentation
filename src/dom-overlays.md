# DOM Overlays

_At the moment, this page is taken verbatim from [https://github.com/projectfluent/fluent.js/wiki/DOM-Overlays](https://github.com/projectfluent/fluent.js/wiki/DOM-Overlays)_

When localizing an HTML document you're likely to encounter two scenarios where the DOM elements may appear in translations:

  - _Text-level elements_. Localizers may want to use some HTML markup to make the translation correct according to the rules of grammar and spelling. For instance, `<em>` may be used for words borrowed from foreign languages, `<sup>` may be used for ordinals or abbreviations, etc.

  - _Functional elements_. Developers may want to pass elements as arguments to the translation and create rich language-agnostic UIs. For instance, they may define an `<img>` element which should be placed inline inside of the translation. Each language will need to decide where exactly the `<img>` should go.

`fluent-dom` features a secure overlay logic which:

  - allows localizers to use some safe text-level markup in translations, and
  - allows developers to pass functional elements as arguments to translations.

## Text-Level Elements

Text-level elements such as `<em>`, `<strong>` and `<sup>`, are considered safe and are in fact often required to build correct translations. `fluent-dom` always allows these elements to be present in translations. No further nesting is allowed and all attributes defined on these text-level elements are sanitized using a well-defined list of safe attributes.

```properties
ordinals = 1<sup>st</sup>, 2<sup>nd</sup>, 3<sup>rd</sup>, and so on.
```

The list of text-level elements is defined by the HTML specification in [§4.5. Text-level semantics](https://www.w3.org/TR/html52/textlevel-semantics.html). `fluent-dom` allows almost all of them by default, with the exception of `<a>` (which doesn't make much sense without `href`) and `<ruby>`, `<rt>` and `<rp>` (which require nesting).

## Functional Elements

Developers may also put child elements (both text-level and others) inside of the element which is the target of the translation. These child elements must be annotated with the `data-l10n-name` attribute. `fluent-dom` will look for corresponding child elements defined by the translation and clone them into the final translated result. The cloning preserves functional attributes defined in the source (`href`, `class`, `src`) but destroys any event listeners attached to the child element. Safe attributes found on the matching child element from the translation will be copied to the resulting child.

### `<img>` Example

```html
<p data-l10n-id="hello-icon">
    <img data-l10n-name="world" src="world.png">
</p>
```
```properties
hello-icon = Hello, <img data-l10n-name="world" alt="world">!
```

Result:

```html
<p data-l10n-id="hello-icon">
    Hello, <img data-l10n-name="world" alt="world" src="world.png">!
</p>
```

### `<a>` Example

```html
<span data-l10n-id="privacy-note">
  <a data-l10n-name="priv" href="https://www.mozilla.org/privacy" />
</span>
```

```properties
privacy-note = Read our <a data-l10n-name="priv" title="Privacy Policy">privacy policy</a>.
```

will produce:

```html
<span data-l10n-id="privacy-note">
  Read our <a data-l10n-name="priv" href="https://www.mozilla.org/privacy" title="Privacy Policy">privacy policy</a>.
</span>
```

## Safety

The DOM Overlays logic sanitizes all elements found in the translation before inserting them into the DOM. Only safe text-level elements are allowed by default. Their attributes are also sanitized to only allow safe translatable attributes like `title` or `alt`.

When non-text-level functional elements are used in the translation, like `<img>`, `fluent-dom` will only try to match them against the source HTML if both the type and the value of the `data-l10n-name` attribute match the corresponding element defined in the source.

This design secures `fluent-dom` against potentially malicious translations. At the same time it empowers the localizers and the developers to make the localized user experience more complete.

### Whitelisting additional attributes

Developers can allow additional attributes to be set by the translation via the `data-l10n-attrs` attribute. Its value should be a comma-separated list of attribute names.

```html
<span data-l10n-id="privacy-note">
  <a href="https://www.mozilla.org/privacy" data-l10n-attrs="style" />
</span>
```

```properties
privacy-note = Read our <a title="Privacy Policy" style="font-weight: bold">privacy policy</a>.
```

will produce:

```html
<span data-l10n-id="privacy-note">
  Read our <a href="https://www.mozilla.org/privacy" data-l10n-attrs="style" title="Privacy Policy" style="font-weight: bold">privacy policy</a>.
</span>
```

Please note that using `data-l10n-attrs` shifts the responsibility for the safety of the widget onto the developer.

## Limitations

The implementation of DOM overlays as of `fluent-dom` 0.2.0 is subject to the following limitations. We plan to address some of them in the future revisions of the feature.

  1. At the moment the identity of functional elements passed into the translation via `data-l10n-name` is not preserved. It's thus not possible to add event listeners to them.

  1. Nested markup is not allowed in either text-level elements or functional elements.

  1. Text content from the translation currently replaces the entire children subtree of functional elements passed into the translation.

  1. There's no way to allow additional elements to be defined in translations without putting them in the source HTML as functional elements.