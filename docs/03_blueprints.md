# 3. Blueprints
[](){ #3 }
[](){ #bp }

This section will focus on Blueprint classes and their internals. When possible, style rules conform to [Epic's Coding Standard](https://docs.unrealengine.com/latest/INT/Programming/Development/CodingStandard).

Remember: Blueprinting badly bears blunders, beware! (Phrase by [KorkuVeren](http://github.com/KorkuVeren))

## Sections

> 3.1 [Compiling][bp-compiling]
> 3.2 [Variables][bp-vars]
> 3.3 [Functions][bp-functions]
> 3.4 [Graphs][bp-graphs]

[](){ #3.1 }
[](){ #bp-compiling }
## 3.1 Compiling

All blueprints should compile with zero warnings and zero errors. You should fix blueprint warnings and errors immediately as they can quickly cascade into very scary unexpected behavior.

Do *not* submit broken blueprints to source control. If you must store them on source control, shelve them instead.

Broken blueprints can cause problems that manifest in other ways, such as broken references, unexpected behavior, cooking failures, and frequent unneeded recompilation. A broken blueprint has the power to break your entire game.

[](){ #3.2 }
[](){ #bp-vars }
## 3.2 Variables

The words `variable` and `property` may be used interchangeably.

### Sections

> 3.2.1 [Naming][bp-vars]
> 3.2.2 [Editable][bp-vars-editable]
> 3.2.3 [Categories][bp-vars-categories]
> 3.2.4 [Access][bp-vars-access]
> 3.2.5 [Advanced][bp-vars-advanced]
> 3.2.6 [Transient][bp-vars-transient]
> 3.2.7 [Config][bp-vars-config]

[](){ #3.2.1 }
[](){ #bp-var-naming }
### 3.2.1 Naming

[](){ #3.2.1.1 }
[](){ #bp-var-naming-nouns }
#### 3.2.1.1 Nouns

All non-boolean variable names must be clear, unambiguous, and descriptive nouns.

[](){ #3.2.1.2 }
[](){ #bp-var-naming-case }
#### 3.2.1.2 PascalCase

All non-boolean variables should be in the form of [PascalCase][terms-cases].

[](){ #3.2.1.2e }
##### 3.2.1.2e Examples:

* `Score`
* `Kills`
* `TargetPlayer`
* `Range`
* `CrosshairColor`
* `AbilityID`

[](){ #3.2.1.3 }
[](){ #bp-var-bool-prefix }
#### 3.2.1.3 Boolean `b` Prefix

All booleans should be named in PascalCase but prefixed with a lowercase `b`.

Example: Use `bDead` and `bEvil`, **not** `Dead` and `Evil`.

UE Blueprint editors know not to include the `b` in user-friendly displays of the variable.

[](){ #3.2.1.4 }
[](){ #bp-var-bool-names }
#### 3.2.1.4 Boolean Names

[](){ #3.2.1.4.1 }
##### 3.2.1.4.1 General And Independent State Information

All booleans should be named as descriptive adjectives when possible if representing general information. Do not include words that phrase the variable as a question, such as `Is`. This is reserved for functions.

Example: Use `bDead` and `bHostile` **not** `bIsDead` and `bIsHostile`.

Try to not use verbs such as `bRunning`. Verbs tend to lead to complex states.

[](){ #3.2.1.4.2 }
##### 3.2.1.4.2 Complex States

Do not to use booleans to represent complex and/or dependent states. This makes state adding and removing complex and no longer easily readable. Use an enumeration instead.

Example: When defining a weapon, do **not** use `bReloading` and `bEquipping` if a weapon can't be both reloading and equipping. Define an enumeration named `EWeaponState` and use a variable with this type named `WeaponState` instead. This makes it far easier to add new states to weapons.

Example: Do **not** use `bRunning` if you also need `bWalking` or `bSprinting`. This should be defined as an enumeration with clearly defined state names.

[](){ #3.2.1.5 }
[](){ #bp-vars-naming-context }
#### 3.2.1.5 Considered Context

All variable names must not be redundant with their context as all variable references in Blueprint will always have context.

[](){ #3.2.1.5e }
##### 3.2.1.5e Examples:

Consider a Blueprint called `PlayerCharacter_BP`.

**Bad**

* `PlayerScore`
* `PlayerKills`
* `MyTargetPlayer`
* `MyCharacterName`
* `CharacterSkills`
* `ChosenCharacterSkin`

All of these variables are named redundantly. It is implied that the variable is representative of the `PlayerCharacter_BP` it belongs to because it is `PlayerCharacter_BP` that is defining these variables.

**Good**

* `Score`
* `Kills`
* `TargetPlayer`
* `Name`
* `Skills`
* `Skin`

[](){ #3.2.1.6 }
[](){ #bp-vars-naming-atomic }
#### 3.2.1.6 Do _Not_ Include Atomic Type Names

Atomic or primitive variables are variables that represent data in their simplest form, such as booleans, integers, floats, and enumerations.

Strings and vectors are considered atomic in terms of style when working with Blueprints, however they are technically not atomic.

> While vectors consist of three floats, vectors are often able to be manipulated as a whole, same with rotators.

> Do _not_ consider Text variables as atomic, they are secretly hiding localization functionality. The atomic type of a string of characters is `String`, not `Text`.

Atomic variables should not have their type name in their name.

Example: Use `Score`, `Kills`, and `Description` **not** `ScoreFloat`, `FloatKills`, `DescriptionString`.

The only exception to this rule is when a variable represents 'a number of' something to be counted _and_ when using a name without a variable type is not easy to read.

Example: A fence generator needs to generate X number of posts. Store X in `NumPosts` or `PostsCount` instead of `Posts` as `Posts` may potentially read as an Array of a variable type named `Post`.

[](){ #3.2.1.7 }
[](){ #bp-vars-naming-complex }
#### 3.2.1.7 Do Include Non-Atomic Type Names

Non-atomic or complex variables are variables that represent data as a collection of atomic variables. Structs, Classes, Interfaces, and primitives with hidden behavior such as `Text` and `Name` all qualify under this rule.

> While an Array of an atomic variable type is a list of variables, Arrays do not change the 'atomicness' of a variable type.

These variables should include their type name while still considering their context.

If a class owns an instance of a complex variable, i.e. if a `PlayerCharacter_BP` owns a `Hat_BP`, it should be stored as the variable type as without any name modifications.

Example: Use `Hat`, `Flag`, and `Ability` **not** `MyHat`, `MyFlag`, and `PlayerAbility`.

If a class does not own the value a complex variable represents, you should use a noun along with the variable type.

Example: If a `Turret_BP` has the ability to target a `PlayerCharacter_BP`, it should store its target as `TargetPlayer` as when in the context of `Turret_BP` it should be clear that it is a reference to another complex variable type that it does not own.


[](){ #3.2.1.8 }
[](){ #bp-vars-naming-arrays }
#### 3.2.1.8 Arrays

Arrays follow the same naming rules as above, but should be named as a plural noun.

Example: Use `Targets`, `Hats`, and `EnemyPlayers`, **not** `TargetList`, `HatArray`, `EnemyPlayerArray`.


[](){ #3.2.2 }
[](){ #bp-vars-editable }
### 3.2.2 Editable Variables

All variables that are safe to change the value of in order to configure behavior of a blueprint should be marked as `Editable`.

Conversely, all variables that are not safe to change or should not be exposed to designers should _not_ be marked as editable, unless for engineering reasons the variable must be marked as `Expose On Spawn`.

Do not arbitrarily mark variables as `Editable`.

[](){ #3.2.2.1 }
[](){ #bp-vars-editable-tooltips }
#### 3.2.2.1 Tooltips

All `Editable` variables, including those marked editable just so they can be marked as `Expose On Spawn`, should have a description in their `Tooltip` fields that explains how changing this value affects the behavior of the blueprint.

[](){ #3.2.2.2 }
[](){ #bp-vars-editable-ranges }
#### 3.2.2.2 Slider And Value Ranges

All `Editable` variables should make use of slider and value ranges if there is ever a value that a variable should _not_ be set to.

Example: A blueprint that generates fence posts might have an editable variable named `PostsCount` and a value of -1 would not make any sense. Use the range fields to mark 0 as a minimum.

If an editable variable is used in a Construction Script, it should have a reasonable Slider Range defined so that someone can not accidentally assign it a large value that could crash the editor.

A Value Range only needs to be defined if the bounds of a value are known. While a Slider Range prevents accidental large number inputs, an undefined Value Range allows a user to specify a value outside the Slider Range that may be considered 'dangerous' but still valid.

[](){ #3.2.3 }
[](){ #bp-vars-categories }
### 3.2.3 Categories

If a class has only a small number of variables, categories are not required.

If a class has a moderate amount of variables (5-10), all `Editable` variables should have a non-default category assigned. A common category is `Config`.

If a class has a large amount of variables, all `Editable` variables should be categorized into sub-categories using the category `Config` as the base category. Non-editable variables should be categorized into descriptive categories describing their usage.

> You can define sub-categories by using the pipe character `|`, i.e. `Config | Animations`.

Example: A weapon class set of variables might be organized as:

    |-- Config
    |    |-- Animations
    |    |-- Effects
    |    |-- Recoil
    |    |-- Sounds
    |    |-- Timings
    |-- Animations
    |-- State
    |-- Visuals

[](){ #3.2.4 }
[](){ #bp-vars-access }
### 3.2.4 Variable Access Level

In C++, variables have a concept of access level. Public means any code outside the class can access the variable. Protected means only the class and any child classes can access this variable internally. Private means only this class and no child classes can access this variable.

Blueprints do not have a defined concept of protected access currently.

Treat `Editable` variables as public variables. Treat non-editable variables as protected variables.

[](){ #3.2.4.1 }
[](){ #bp-vars-access-private }
#### 3.2.4.1 Private Variables

Unless it is known that a variable should only be accessed within the class it is defined and never a child class, do not mark variables as private. Until variables are able to be marked `protected`, reserve private for when you absolutely know you want to restrict child class usage.

[](){ #3.2.5 }
[](){ #bp-vars-advanced }
### 3.2.5 Advanced Display

If a variable should be editable but often untouched, mark it as `Advanced Display`. This makes the variable hidden unless the advanced display arrow is clicked.

To find the `Advanced Display` option, it is listed as an advanced displayed variable in the variable details list.

[](){ #3.2.6 }
[](){ #bp-vars-transient }
### 3.2.6 Transient Variables

Transient variables are variables that do not need to have their value saved and loaded and have an initial value of zero or null. This is useful for references to other objects and actors who's value isn't known until run-time. This prevents the editor from ever saving a reference to it, and speeds up saving and loading of the blueprint class.

Because of this, all transient variables should always be initialized as zero or null. To do otherwise would result in hard to debug errors.

[](){ #3.2.7 }
[](){ #bp-vars-config }
### 3.2.8 Config Variables

Do not use the `Config Variable` flag. This makes it harder for designers to control blueprint behavior. Config variables should only be used in C++ for rarely changed variables. Think of them as `Advanced Advanced Display` variables.

[](){ #3.3 }
[](){ #bp-functions }
## 3.3 Functions, Events, and Event Dispatchers

This section describes how you should author functions, events, and event dispatchers. Everything that applies to functions also applies to events, unless otherwise noted.

[](){ #3.3.1 }
[](){ #bp-funcs-naming }
### 3.3.1 Function Naming

The naming of functions, events, and event dispatchers is critically important. Based on the name alone, certain assumptions can be made about functions. For example:

* Is it a pure function?
* Is it fetching state information?
* Is it a handler?
* Is it an RPC?
* What is its purpose?

These questions and more can all be answered when functions are named appropriately.

[](){ #3.3.1.1 }
[](){ #bp-funcs-naming-verbs }
### 3.3.1.1 All Functions Should Be Verbs

All functions and events perform some form of action, whether its getting info, calculating data, or causing something to explode. Therefore, all functions should all start with verbs. They should be worded in the present tense whenever possible. They should also have some context as to what they are doing.

`OnRep` functions, event handlers, and event dispatchers are an exception to this rule.

Good examples:

* `Fire` - Good example if in a Character / Weapon class, as it has context. Bad if in a Barrel / Grass / any ambiguous class.
* `Jump` - Good example if in a Character class, otherwise, needs context.
* `Explode`
* `ReceiveMessage`
* `SortPlayerArray`
* `GetArmOffset`
* `GetCoordinates`
* `UpdateTransforms`
* `EnableBigHeadMode`
* `IsEnemy` - ["Is" is a verb.](http://writingexplained.org/is-is-a-verb)

Bad examples:

* `Dead` - Is Dead? Will deaden?
* `Rock`
* `ProcessData` - Ambiguous, these words mean nothing.
* `PlayerState` - Nouns are ambiguous.
* `Color` - Verb with no context, or ambiguous noun.

[](){ #3.3.1.2 }
[](){ #bp-funcs-naming-onrep }
### 3.3.1.2 Property RepNotify Functions Always `OnRep_Variable`

All functions for replicated with notification variables should have the form `OnRep_Variable`. This is forced by the Blueprint editor. If you are writing a C++ `OnRep` function however, it should also follow this convention when exposing it to Blueprints.

[](){ #3.3.1.3 }
[](){ #bp-funcs-naming-bool }
### 3.3.1.3 Info Functions Returning Bool Should Ask Questions

When writing a function that does not change the state of or modify any object and is purely for getting information, state, or computing a yes/no value, it should ask a question. This should also follow [the verb rule][bp-funcs-naming-verbs].

This is extremely important as if a question is not asked, it may be assumed that the function performs an action and is returning whether that action succeeded.

Good examples:

* `IsDead`
* `IsOnFire`
* `IsAlive`
* `IsSpeaking`
* `IsHavingAnExistentialCrisis`
* `IsVisible`
* `HasWeapon` - ["Has" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)
* `WasCharging` - ["Was" is past-tense of "be".](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html) Use "was" when referring to 'previous frame' or 'previous state'.
* `CanReload` - ["Can" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)

Bad examples:

* `Fire` - Is on fire? Will fire? Do fire?
* `OnFire` - Can be confused with event dispatcher for firing.
* `Dead` - Is dead? Will deaden?
* `Visibility` - Is visible? Set visibility? A description of flying conditions?

[](){ #3.3.1.4 }
[](){ #bp-funcs-naming-eventhandlers }
### 3.3.1.4 Event Handlers and Dispatchers Should Start With `On`

Any function that handles an event or dispatches an event should start with `On` and continue to follow [the verb rule][bp-funcs-naming-verbs]. The verb may move to the end however if past-tense reads better.

[Collocations](http://dictionary.cambridge.org/us/grammar/british-grammar/about-words-clauses-and-sentences/collocation) of the word `On` are exempt from following the verb rule.

`Handle` is not allowed. It is 'Unreal' to use `On` instead of `Handle`, while other frameworks may prefer to use `Handle` instead of `On`.

Good examples:

* `OnDeath` - Common collocation in games
* `OnPickup`
* `OnReceiveMessage`
* `OnMessageRecieved`
* `OnTargetChanged`
* `OnClick`
* `OnLeave`

Bad examples:

* `OnData`
* `OnTarget`
* `HandleMessage`
* `HandleDeath`

[](){ #3.3.1.5 }
[](){ #bp-funcs-naming-rpcs }
### 3.3.1.5 Remote Procedure Calls Should Be Prefixed With Target

Any time an RPC is created, it should be suffixed with either `Server`, `Client`, or `Multicast`. No exceptions.

After the suffix, follow all other rules regarding function naming.

Good examples:

* `FireWeaponServer`
* `NotifyDeathClient`
* `SpawnTracerEffectMulticast`

Bad examples:

* `FireWeapon` - Does not indicate its an RPC of some kind.
* `ServerClientBroadcast` - Confusing.
* `AllNotifyDeath` - Use `Multicast`, never `All`.
* `ClientWeapon` - No verb, ambiguous.


[](){ #3.3.2 }
[](){ #bp-funcs-return }
### 3.3.2 All Functions Must Have Return Nodes

All functions must have return nodes, no exceptions.

Return nodes explicitly note that a function has finished its execution. In a world where blueprints can be filled with `Sequence`, `ForLoopWithBreak`, and backwards reroute nodes, explicit execution flow is important for readability, maintenance, and easier debugging.

The Blueprint compiler is able to follow the flow of execution and will warn you if there is a branch of your code with an unhandled return or bad flow if you use return nodes.

In situations like where a programmer may add a pin to a Sequence node or add logic after a for loop completes but the loop iteration might return early, this can often result in an accidental error in code flow. The warnings the Blueprint compiler will alert everyone of these issues immediately.

[](){ #3.3.3 }
[](){ #bp-graphs-funcs-node-limit }
### 3.3.3 No Function Should Have More Than 50 Nodes

Simply, no function should have more than 50 nodes. Any function this big should be broken down into smaller functions for readability and ease of maintenance.

The following nodes are not counted as they are deemed to not increase function complexity:

* Comment
* Route
* Cast
* Getting a Variable
* Breaking a Struct
* Function Entry
* Self

[](){ #3.3.4 }
[](){ #bp-graphs-funcs-description }
### 3.3.4 All Public Functions Should Have A Description

This rule applies more to public facing or marketplace blueprints, so that others can more easily navigate and consume your blueprint API.

Simply, any function that has an access specificer of Public should have its description filled out.

[](){ #3.3.5 }
[](){ #bp-graphs-funcs-plugin-category }
### 3.3.5 All Custom Static Plugin `BlueprintCallable` Functions Must Be Categorized By Plugin Name

If your project includes a plugin that defines `static` `BlueprintCallable` functions, they should have their category set to the plugin's name or a subset category of the plugin's name.

For example, `Zed Camera Interface` or `Zed Camera Interface | Image Capturing`.

[](){ #3.4 }
[](){ #bp-graphs }
## 3.4 Blueprint Graphs

This section covers things that apply to all Blueprint graphs.

[](){ #3.4.1 }
[](){ #bp-graphs-spaghetti }
### 3.4.1 No Spaghetti

Wires should have clear beginnings and ends. You should never have to mentally untangle wires to make sense of a graph. Many of the following sections are dedicated to reducing spaghetti.

[](){ #3.4.2 }
[](){ #bp-graphs-align-wires }
### 3.4.2 Align Wires Not Nodes

Always align wires, not nodes. You can't always control the size and pin location on a node, but you can always control the location of a node and thus control the wires. Straight wires provide clear linear flow. Wiggly wires wear wits wickedly. You can straighten wires by using the Straighten Connections command with BP nodes selected. Hotkey: Q

Good example: The tops of the nodes are staggered to keep a perfectly straight white exec line.
![Aligned By Wires](https://github.com/Allar/ue5-style-guide/blob/main/images/bp-graphs-align-wires-good.png?raw=true "Aligned By Wires")

Bad Example: The tops of the nodes are aligned creating a wiggly white exec line.
![Bad](https://github.com/Allar/ue5-style-guide/blob/main/images/bp-graphs-align-wires-bad.png?raw=true "Wiggly")

Acceptable Example: Certain nodes might not cooperate no matter how you use the alignment tools. In this situation, try to minimize the wiggle by bringing the node in closer.
![Acceptable](https://github.com/Allar/ue5-style-guide/blob/main/images/bp-graphs-align-wires-acceptable.png?raw=true "Acceptable")

[](){ #3.4.3 }
[](){ #bp-graphs-exec-first-class }
### 3.4.3 White Exec Lines Are Top Priority

If you ever have to decide between straightening a linear white exec line or straightening data lines of some kind, always straighten the white exec line.

[](){ #3.4.4 }
[](){ #bp-graphs-block-comments }
### 3.4.4 Graphs Should Be Reasonably Commented

Blocks of nodes should be wrapped in comments that describe their higher-level behavior. While every function should be well named so that each individual node is easily readable and understandable, groups of nodes contributing to a purpose should have their purpose described in a comment block. If a function does not have many blocks of nodes and its clear that the nodes are serving a direct purpose in the function's goal, then they do not need to be commented as the function name and  description should suffice.

[](){ #3.4.5 }
[](){ #bp-graphs-cast-error-handling }
### 3.4.5 Graphs Should Handle Casting Errors Where Appropriate

If a function or event assumes that a cast always succeeds, it should appropriately report a failure in logic if the cast fails. This lets others know why something that is 'supposed to work' doesn't. A function should also attempt a graceful recover after a failed cast if it's known that the reference being casted could ever fail to be casted.

This does not mean every cast node should have its failure handled. In many cases, especially events regarding things like collisions, it is expected that execution flow terminates on a failed cast quietly.

[](){ #3.4.6 }
[](){ #bp-graphs-dangling-nodes }
### 3.4.6 Graphs Should Not Have Any Dangling / Loose / Dead Nodes

All nodes in all blueprint graphs must have a purpose. You should not leave dangling blueprint nodes around that have no purpose or are not executed.
