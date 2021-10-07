# Fluent.js

Fluent.js is a JavaScript implementation of Project Fluent, a localization framework designed to unleash the expressive power of the natural language.

Fluent.js allows interaction with [`data-l10n-id`](./l10n-id.md) and [`data-l10n-args`](./l10n-args.md) through the [`DOMLocalization`](./dom-localization.md) class, which is derived from the [`Localization`](localization.md) base class.

The `Localization` base class provides the mid-level APIs for interacting with Fluent. High-level abstractions such as Fluent DOM (for localizing HTML pages) and Fluent React (for react projects) are built on top of this `Localization` object's abstractions.
