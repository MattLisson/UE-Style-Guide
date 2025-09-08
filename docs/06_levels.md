# 6. Levels / Maps
[](){ #6 }
[](){ #Levels }
[](){ #levels }

[See Terminology Note][terms-level-map] regarding "levels" vs "maps".

This section will focus on Level assets and their internals.


[](){ #6.1 }
[](){ #levels-no-errors-or-warnings }
## 6.1 No Errors Or Warnings

All levels should load with zero errors or warnings. If a level loads with any errors or warnings, they should be fixed immediately to prevent cascading issues.

You can run a map check on an open level in the editor by using the console command "map check".

[](){ #6.2 }
[](){ #levels-lighting-should-be-built }
## 6.2 Lighting Should Be Built

It is normal during development for levels to occasionally not have lighting built. When doing a test/internal/shipping build or any build that is to be distributed however, lighting should always be built.

[](){ #6.3 }
[](){ #levels-no-visible-z-fighting }
## 6.3 No Player Visible Z Fighting

Levels should not have any [z-fighting](https://en.wikipedia.org/wiki/Z-fighting) in all areas visible to the player.

[](){ #6.4 }
[](){ #levels-mp-rules }
## 6.4 Marketplace Specific Rules

If a project is to be sold on the UE Marketplace, it must follow these rules.

[](){ #6.4.1 }
[](){ #levels-mp-rules-overview }
### 6.4.1 Overview Level

If your project contains assets that should be visualized or demoed, you must have a map within your project that contains the name "Overview".

This overview map, if it is visualizing assets, should be set up according to [Epic's guidelines](http://help.epicgames.com/customer/en/portal/articles/2592186-marketplace-submission-guidelines-preparing-your-assets#Required%20Levels%20and%20Maps).

For example, `InteractionComponent_Overview`.

[](){ #6.4.2 }
[](){ #levels-mp-rules-demo }
### 6.4.2 Demo Level

If your project contains assets that should be demoed or come with some sort of tutorial, you must have a map within your project that contains the name "Demo". This level should also contain documentation within it in some form that illustrates how to use your project. See Epic's Content Examples project for good examples on how to do this.

If your project is a gameplay mechanic or other form of system as opposed to an art pack, this can be the same as your "Overview" map.

For example, `InteractionComponent_Overview_Demo`, `ExplosionKit_Demo`.
