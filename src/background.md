# Background

Fluent aims to provide useful abstractions over the entire process of localization. 
It is helpful to view the process as divided into three layers: low level, mid level and high level.

## Low Level: Bundle Generation

At the lowest level of abstraction, Fluent expects to operate on `bundles` of `resources`. 

In this context, a `resource` is a Fluent Translation List (`.ftl`) file that contains translations of localized messages.

A `bundle` can be seen as a collection of `resources` that provide a set of translations for a given locale. 

The process of fetching `resources` and collecting them into `bundles` is an incredibly complex space that may have different desired implementations for different systems, which is why it deserves its own layer of abstraction.

## Mid Level: The Localization Class

Sitting on top of the abstracted low-level mechanism to fetch `bundles` of localization `resources` is the `Localization` class. 

The separation of abstraction between the low-level and mid-level allows the `Localization` API
to be agnostic of how the resources are retrieved. The resources themselves could be sitting 
on the file system, fetched asynchronously over a network, or something else entirely.

Once the `Localization` class is given `bundles` to work with, it provides an API to translate localized messages based on the data contained within the bundles. 

## High Level: DOM Localization and Friends

Sitting on top of the abstracted low-level and mid-level mechanisms to retrieve resources and 
format localized messages is the `DOMLocalization` class. 

In this abstraction layer, the `DOMLocalization` provides an API that works natively with HTML elements and fragments. It allows you to declaratively localize content by adding attributes directly into HTML.

Importantly, `DOMLocalization` is only one of many high-level abstractions that can sit on top of the low-level and mid-level layers. Other high-level abstractions such as [`Fluent React`](https://github.com/projectfluent/fluent.js/tree/master/fluent-react#fluentreact-) can just as well sit on top of the previous layers, providing a clean API to work with `ReactJS`
