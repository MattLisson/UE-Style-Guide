# Introduction

*A mostly reasonable approach to Unreal Engine 4 & 5*

Heavily inspired by the [Airbnb Javascript Style Guide](https://github.com/airbnb/javascript) and forked from [Allar's UE style guide](http://UE.style/).

## Important Terminology

[](){ #terms-level-map }
##### Levels/Maps

The word 'map' generally refers to what the average person calls a 'level' and may be used interchangeably. See this term's history [here](https://en.wikipedia.org/wiki/Level_(video_gaming)).

[](){ #terms-identifiers }
##### Identifiers
An `Identifier` is anything that resembles or serves as a "name". For example, the name of an asset, or the name of a material later, or a blueprint property, a variable, or a folder name, or for a data table row name, etc...

[](){ #terms-cases }
##### Cases

There are a few different ways you can `CaseWordsWhenNaming`. Here are some common casing types:

> ###### PascalCase
>
> Capitalize every word and remove all spaces, e.g. `DesertEagle`, `StyleGuide`, `ASeriesOfWords`.
>
> ###### camelCase
>
> The first letter is always lowercase but every following word starts with uppercase, e.g. `desertEagle`, `styleGuide`, `aSeriesOfWords`.
>
> ###### Snake_case
>
> Words can arbitrarily start upper or lowercase but words are separated by an underscore, e.g. `desert_eagle`, `Style_Guide`, `a_Series_of_Words`.

[](){ #terms-var-prop }
##### Variables / Properties

The words 'variable' and 'property' in most contexts are interchangable. If they are both used together in the same context however:

[](){ #terms-property }
###### Property
Usually refers to a variable defined in a class. For example, if `Barrel_BP` had a variable `bExploded`, `bExploded` may be referred to as a property of `Barrel_BP`.

When in the context of a class, it is often used to imply accessing previously defined data.

[](){ #terms-variable }
###### Variable
Usually refers to a variable defined as a function argument or a local variable inside a function.

When in the context of a class, it is often used to convey discussion about its definition and what it will hold.


## Major Contributors

* [Michael Allar](http://allarsblog.com): [GitHub](https://github.com/Allar), [Twitter](https://twitter.com/michaelallar)
* [CosmoMyzrailGorynych](https://github.com/CosmoMyzrailGorynych)
* [billymcguffin](https://github.com/billymcguffin)
* [akenatsu](https://github.com/akenatsu)

## License

Copyright (c) 2016 Gamemakin LLC

See [LICENSE](LICENSE)

