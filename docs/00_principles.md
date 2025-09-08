# 0. Principles
[](){ #0 }

These principles have been adapted from [idomatic.js style guide](https://github.com/rwaldron/idiomatic.js/).

[](){ #0.1 }
## 0.1 If your UE project already has a style guide, you should follow it.

If you are working on a project or with a team that has a pre-existing style guide, it should be respected. Any inconsistency between an existing style guide and this guide should defer to the existing.

Style guides should be living documents. You should propose style guide changes to an existing style guide as well as this guide if you feel the change benefits all usages.

> #### "Arguments over style are pointless. There should be a style guide, and you should follow it."
> [_Rebecca Murphey_](https://rmurphey.com)

[](){ #0.2 }
## 0.2 All structure, assets, and code in any Unreal Engine project should look like a single person created it, no matter how many people contributed

Moving from one project to another should not cause a re-learning of style and structure. Conforming to a style guide removes unneeded guesswork and ambiguities.

It also allows for more productive creation and maintenance as one does not need to think about style. Simply follow the instructions. This style guide is written with best practices in mind, meaning that by following this style guide you will also minimize hard to track issues.

[](){ #0.3 }
## 0.3 Friends do not let friends have bad style.

If you see someone working either against a style guide or no style guide, try to correct them.

When working within a team or discussing within a community such as [Unreal Slackers](http://join.unrealslackers.org/), it is far easier to help and to ask for help when people are consistent. Nobody likes to help untangle someone's Blueprint spaghetti or deal with assets that have names they can't understand.

If you are helping someone whose work conforms to a different but consistent and sane style guide, you should be able to adapt to it. If they do not conform to any style guide, please direct them here.

[](){ #00 }
## 0.4 Globally Enforced Opinions

[](){ #00.1 }
### 0.4.1 Forbidden Characters

#### Identifiers

In any `Identifier` of any kind, **never** use the following unless absolutely forced to:

* White space of any kind
* Backward slashes `\`
* Symbols i.e. `#!@$%`
* Any Unicode character

Any `Identifier` should strive to only have the following characters when possible (the RegEx `[A-Za-z0-9_]+`)

* ABCDEFGHIJKLMNOPQRSTUVWXYZ
* abcdefghijklmnopqrstuvwxyz
* 1234567890
* _ (sparingly)

The reasoning for this is this will ensure the greatest compatibility of all data across all platforms across all tools, and help prevent downtime due to potentially bad character handling for identifiers in code you don't control.
