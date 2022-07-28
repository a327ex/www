+++
title = "Super Auto Pets mechanics"
tags = [
    "design",
]
date = "2022-07-28"
images = ["https://i.imgur.com/mm058gj.png"]
+++

## Start

I've been playing a lot of Super Auto Pets recently. I was kinda late to play it because last year when it came out I was quite auto battler fatigued, so I couldn't bring myself to try it.
But I finally tried it like 2 months ago and have about 100 hours in it since then and I really really like it.

This is a good place for me to write this post because my thoughts on it are freshest, and I've already gotten most analytical insights I'll get even though I'm going to keep playing it for 
hundreds of hours more most likely. And this happens because there are diminishing returns to such insights, since I've learned the most from the first 100 hours and subsequent ones will each teach less.

One example of this is that I distinctly remember the first ~10-20 hours of SAP feeling *alien* to me. I don't think I've ever played a game that had quite this combination of mechanics
(and by mechanics I mean what each unit does, not the fact that it's an auto battler or that it has a rerolling shop) so they all felt very distinctly weird to me until it all started connecting.

So I'm going to spend this post going over every unit in the game and generalizing the mechanics.
SAP has a lot of unique and good ideas that are very easily transferable to any game that is built around a rerolling shop (like SNKRX, Brotato, Just King, Underlords, TFT, etc) so it's worth it to go through it thoroughly.

## Tier 1

[⬆️ Start](#start)  
[1️⃣ Tier 1](#tier-1)  
[2️⃣ Tier 2](#tier-2)  
[3️⃣ Tier 3](#tier-3)  
[4️⃣ Tier 4](#tier-4)  
[6️⃣ Tier 6](#tier-6)  
[5️⃣ Tier 5](#tier-5)  
[⬇️ Final tables](#final-tables)  
[⬇️ Rerolling shop genre](#rerolling-shop-genre)  

### Ant

{{< figure src="https://i.imgur.com/JVhmemC.png" >}}

The most sensible way of dividing SAP's mechanics are in terms of **triggers** and **effects**. In the ant's case, its trigger is faint and its effect is a stat change to a random ally.
It also seems from the ant's effect that effects in general should have two variables: what the effect is and its target.

Both the faint trigger and the stat change effect also behave differently depending on whether they happen in or out of combat. They are temporary for the former and permanent for the latter.
This particular idea is something that is game specific that I'm going to largely ignore, even though it applies to a lot of the game's mechanics.

This is because I can easily imagine a game where the difference between in and out of combat are irrelevant. For instance, if in your rerolling shop game units always die permanently when they die,
then it makes no sense for there to be a difference in how faint behaves. 

The same goes for another trigger like hurt. If units are always hurt permanently when they are hurt, then it makes no sense
for the hurt trigger to behave differently.
So given that this is game specific and it has no effect on the mechanic itself whatsoever, it can be safely ignored.

So from the ant we could start with something like this:

| Trigger | Description |
| --- | --- |
| `Faint` | `when a unit dies` |

| Effect | Description |
| --- | --- |
| `Stat change` | `add, sub, mul or div of a stat` | 

| Effect target | Description |
| --- | --- |
| `Random ally` | `a random ally` |

The way to build a unit generally is to take one thing from each table. So the ant would be something like:

* Trigger: faint
* Effect: stat change
* Effect target: random ally

And the point of laying out the game's mechanics in tables like this is that it makes it easier to visualize and then iterate upon, provided you've chosen the right level of abstraction
for your tables. In this case, triggers and effects are very obviously right, so it will work OK.

### Beaver

{{< figure src="https://i.imgur.com/GdQivPs.png" >}}

| Trigger | Description |
| --- | --- |
| Faint | when the unit dies |
| `Sell` | `when the unit is sold` |

| Effect target | Description |
| --- | --- |
| `N random allies` | `where N >= 1` |

Just a small change from the previous `random ally` effect target to avoid having to repeat it in the table for multiple targets. The beaver would look like this:

* Trigger: sell
* Effect: stat change
* Effect target: 2 random allies

I'm not going to repeat this for every unit. For units where a new trigger/effect/effect target exists, I'll just add the new element and it will be `bolded like this`. 
And for units that can be built from elements that were previously added then I'll show how they should be built instead.

### Cricket

{{< figure src="https://i.imgur.com/YmiVoA5.png" >}}

| Effect | Description |
| --- | --- |
| Stat change | add, sub, mul or div of a stat | 
| `Summon` | `summons another unit` |

### Duck

{{< figure src="https://i.imgur.com/zqzeXIp.png" >}}

| Effect target | Description |
| --- | --- |
| `All shop units` | |
| N random allies | where N >= 1 |

### Fish

{{< figure src="https://i.imgur.com/aBftscn.png" >}}

| Trigger | Description |
| --- | --- |
| Faint | when the unit dies |
| `Level-up` | `when the unit levels up` |
| Sell | when the unit is sold |

### Horse

{{< figure src="https://i.imgur.com/cNfmwg9.png" >}}

Here we have a new effect type which has a condition (until the end of battle) attached to it.
I know that the right move is to separate conditions into their own table because there are going to be more (at least I think so), so that's what I'll do here.

| Trigger | Description |
| --- | --- |
| `Ally summoned` | `when an ally is summoned` |
| Faint | when the unit dies |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |

| Effect condition | Description |
| --- | --- |
| `Until the end of battle` | `the effect will persist until the next battle ends` |

| Effect target | Description |
| --- | --- |
| All shop units | |
| `All summoned allies` | |
| N random allies | where N >= 1 |

The problem with `ally summoned` is that it inherently ties itself to the effect target, in this case, the ally that was summoned.
This makes it less composable, so initially I decided to add an `N summoned allies` effect target instead to see how it goes.

The problem with `N summoned allies` though is that it was just wrong. For instance, if we wanted to describe the horse
using it we could do something like "Ally summoned -> Give 1 summoned ally +N attack until the end of battle". But this is wrong,
because it implies that the horse only gives the buff to 1 summoned ally, instead of any ally that is summoned.

Which means that I actually needed to add `all summoned allies` instead as an effect target. But can `all summoned allies` be composed with triggers other than `ally summoned`?
Kind of. I can initially imagine a unit like "Level-up -> Give all summoned allies +N attack". The problem is that this wouldn't be immediate, because unless a unit is summoned when the level up happens
nothing will happen since there will be no targets.

A way to fix this is to add an effect condition like `this turn`. So we would change our imagined unit to "Level-up -> Give all allies summoned this turn +N attack". This makes what it does
clear and also seems to compose well with other triggers. This also makes the `N summoned allies` effect target work, for instance "Level-up -> Give 2 allies summoned this turn +N attack".

This little derail is a good example of why it's good to go through a game's mechanics like this. You can't ignore details and you also get the opportunity to think very clearly about the game
and how you would use its ideas in your own games.

For the types of games that I want to make, which are build heavy games, I'm also always looking at the question of "how can this mechanic be made more composable"
because when you manage to answer that question correctly you get a lot of gameplay out of relatively simple coding.

### Mosquito

{{< figure src="https://i.imgur.com/WU76NOv.png" >}}

| Trigger | Description |
| --- | --- |
| Ally summoned | when an ally is summoned |
| Faint | when the unit dies |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| `Start of battle ` | `when the battle starts` |

| Effect | Description |
| --- | --- |
| `Deal damage` | `deals damage to a unit` |
| Stat change | add, sub, mul or div of a stat | 
| Summon | summons another unit |

| Effect target | Description |
| --- | --- |
| All shop units | |
| All summoned allies | |
| N random allies | where N >= 1 |
| `N random enemies` | `where N >= 1` |

### Otter

{{< figure src="https://i.imgur.com/H9Ok4ly.png" >}}

| Trigger | Description |
| --- | --- |
| Ally summoned | when an ally is summoned |
| `Buy` | `when the unit is bought` |
| Faint | when the unit dies |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |

### Pig 

{{< figure src="https://i.imgur.com/dbNYmg8.png" >}}

| Effect | Description |
| --- | --- |
| Deal damage | deals damage to a unit |
| `Player resource change` | `add, sub, mul or div of a player resource value` |
| Stat change | add, sub, mul or div of a stat | 
| Summon | summons another unit |

Because this is meant for other games, we can more generally define any non-unit stat such as gold as a "player resource".

### Beetle

{{< figure src="https://i.imgur.com/DJO1adl.png" >}}

| Trigger | Description |
| --- | --- |
| Ally summoned | when an ally is summoned |
| Buy | when the unit is bought |
| `Consumes item` | `when the unit is given an item` |
| Faint | when the unit dies |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |

| Effect target | Description |
| --- | --- |
| All shop units | |
| All summoned allies | |
| `Nth shop unit` | `where N >= 1` |
| N random allies | where N >= 1 |
| N random enemies | where N >= 1 |

Because this is meant for other games, we're calling "shop food" an item instead, since it's a more general description of the same idea for most rerolling shop games.

### Bluebird

{{< figure src="https://i.imgur.com/EILq00F.png" >}}

| Trigger | Description |
| --- | --- |
| Ally summoned | when an ally is summoned |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| `End turn` | `when the current turn (shop round) ends, but before battle` |
| Faint | when the unit dies |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |

### Ladybug

{{< figure src="https://i.imgur.com/CIfr15l.png" >}}

| Trigger | Description |
| --- | --- |
| Ally summoned | when an ally is summoned |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Faint | when the unit dies |
| `Item bought` | `when an item is bought` |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |

| Effect target | Description |
| --- | --- |
| All shop units | |
| All summoned allies | |
| Nth shop unit | where N >= 1 |
| N random allies | where N >= 1 |
| N random enemies | where N >= 1 |
| `Self` | `applies to the unit that triggered it` |

### Cockroach

{{< figure src="https://i.imgur.com/aCyd7hg.png" >}}

| Trigger | Description |
| --- | --- |
| Ally summoned | when an ally is summoned |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Faint | when the unit dies |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| `Start of turn` | `when the turn (shop round) starts` |

| Effect | Description |
| --- | --- |
| Deal damage | deals damage to a unit |
| Player resource change | add, sub, mul or div of a player resource value |
| Stat change | add, sub, mul or div of a stat | 
| `Stat set` | `sets a stat to a specific value` |
| Summon | summons another unit |

### Duckling

{{< figure src="https://i.imgur.com/hV22UJW.png" >}}

The first unit where nothing new is needed to describe it. It can be described as:

* Trigger: sell
* Effect: stat change
* Effect target: 1st shop unit

### Frog

{{< figure src="https://i.imgur.com/XK4XUPY.png" >}}

| Effect | Description |
| --- | --- |
| Deal damage | deals damage to a unit |
| Player resource change | add, sub, mul or div of a player resource value |
| `Multiple stat swap` | `swaps stats between multiple units` |
| Stat change | add, sub, mul or div of a stat | 
| Stat set | sets a stat to a specific value |
| Summon | summons another unit |

| Effect target | Description |
| --- | --- |
| All shop units | |
| All summoned allies | |
| Nth shop unit | where N >= 1 |
| N random allies | where N >= 1 |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| `Two adjacent allies` | `applies to 2 allies adjacent to the one that triggered it` |

For SAP specifically there's a distinction between swapping of stats between multiple units (such as with the frog) vs. swapping of stats within a single unit (such as with lollipop).
As these are different effects they should be separate in the effects table.

### Hummingbird

{{< figure src="https://i.imgur.com/2TA0Edk.png" >}}

| Effect target | Description |
| --- | --- |
| All shop units | |
| All summoned allies | |
| Nth shop unit | where N >= 1 |
| N random allies | where N >= 1 |
| `N random classed allies` | `where N >= 1, classed ally = of a specific class` |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

"Strawberry friend" is too specific to SAP to be useful, so instead the more general `classed ally` is used, which means an ally of a given specific class, since auto battlers generally have the auto-chess class mechanic.

### Iguana

{{< figure src="https://i.imgur.com/oPpw5O4.png" >}}

| Trigger | Description |
| --- | --- |
| Ally summoned | when an ally is summoned |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| `Enemy summoned` | `when an enemy is summoned` |
| `Enemy pushed` | `when an enemy is pushed` |
| Faint | when the unit dies |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |

| Effect target | Description |
| --- | --- |
| All shop units | |
| All summoned allies | |
| `All pushed enemies` | |
| `All summoned enemies` | |
| Nth shop unit | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

Similarly to `ally summoned`, `enemies summoned` and `enemies pushed` tie themselves to the effect target, making them less composable. The fix is the same as before.

### Kiwi

{{< figure src="https://i.imgur.com/sLgCNTx.png" >}}

Nothing new.

* Trigger: sell
* Effect: stat change
* Effect target: 1 random classed ally

### Mouse

{{< figure src="https://i.imgur.com/eVIoTvW.png" >}}

| Effect | Description |
| --- | --- |
| Deal damage | deals damage to a unit |
| Player resource change | add, sub, mul or div of a player resource value |
| Multiple stat swap | swaps stats between multiple units |
| `Replace item` | `replaces shop items with other items` |
| Stat change | add, sub, mul or div of a stat | 
| Stat set | sets a stat to a specific value |
| Summon | summons another unit |

### Pillbug

{{< figure src="https://i.imgur.com/Z1JdKcd.png" >}}

| Trigger | Description |
| --- | --- |
| Ally summoned | when an ally is summoned |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| `Upgrade shop tier` | `when the shop levels up` |

| Effect target | Description |
| --- | --- |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| Nth shop unit | where N >= 1 |
| `N allies behind` | `where N >= 1` |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

This has a SAP specific concept that also happens to work for SNKRX, but that might not necessarily work for other shop rerolling games, which is "behind". For games where "behind" doesn't make sense
it can be changed to "to the left/right/up/down" or whatever other type of unit neighborhood set up that makes sense.

### Seahorse

{{< figure src="https://i.imgur.com/8JjcbZR.png" >}}

| Effect | Description |
| --- | --- |
| Deal damage | deals damage to a unit |
| Player resource change | add, sub, mul or div of a player resource value |
| Multiple stat swap | swaps stats between multiple units |
| `Push enemy` | `pushes an enemy to a different position` |
| Replace item | replaces shop items with other items |
| Stat change | add, sub, mul or div of a stat | 
| Stat set | sets a stat to a specific value |
| Summon | summons another unit |

### Chinchilla

{{< figure src="https://i.imgur.com/VY8QUd8.png" >}}

Nothing new.

* Trigger: sell
* Effect: summon

### Frilled Dragon

{{< figure src="https://i.imgur.com/JafhaHl.png" >}}

| Effect condition | Description |
| --- | --- |
| `Per specific ally` | `applies the effect based on the number of allies of a specific type` |
| Until the end of battle | the effect will persist until the next battle ends |

Kind of a weird condition, but this is the most composable version of it I think. Another variation of it would be `per classed ally`, which would apply based on the number of allies of a given class.


### Marmoset

{{< figure src="https://i.imgur.com/ZFopBWi.png" >}}

| Effect | Description |
| --- | --- |
| Deal damage | deals damage to a unit |
| Player resource change | add, sub, mul or div of a player resource value |
| Multiple stat swap | swaps stats between multiple units |
| Push enemy | pushes an enemy to a different position |
| Replace item | replaces shop items with other items |
| `Roll shop` | `rolls the shop` |
| Stat change | add, sub, mul or div of a stat | 
| Stat set | sets a stat to a specific value |
| Summon | summons another unit |

### Moth

{{< figure src="https://i.imgur.com/IrsaR26.png" >}}

| Effect target | Description |
| --- | --- |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| `Nth ally` | `where N >= 1` |
| Nth shop unit | where N >= 1 |
| N allies behind | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Apple

{{< figure src="https://i.imgur.com/8WgBjQt.png" >}}

Items should be described just like units but focused on their effects, generally because they don't have triggers. 
You could try to describe them in a more complex manner, because you could also try to take into account when they're held vs. when they apply instantly, but that adds unnecessary complexity for little gain.

So the apple, for instance, can just be described by its effect, which is a simple stat change.

### Honey

{{< figure src="https://i.imgur.com/1HT6MM0.png" >}}

* Effect: summon

### Peach

{{< figure src="https://i.imgur.com/5zwkMDV.png" >}}

* Effect: stat change

### Strawberry

{{< figure src="https://i.imgur.com/QCZRVfl.png" >}}

| Effect | Description |
| --- | --- |
| `Classify` | `adds a class to a unit` |
| Deal damage | deals damage to a unit |
| Player resource change | add, sub, mul or div of a player resource value |
| Multiple stat swap | swaps stats between multiple units |
| Push enemy | pushes an enemy to a different position |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat set | sets a stat to a specific value |
| Summon | summons another unit |

Keeping up with the theme that strawberry is equivalent to classes in other auto battlers, it makes sense to add the `classify` effect, which acts
very similarly to items in Underlods that can add a new class to a unit.

### Bacon

{{< figure src="https://i.imgur.com/Fb1A0Es.png" >}}

* Effect: stat change 

### Cookie

{{< figure src="https://i.imgur.com/bgG7IUA.png" >}}

* Effect: stat change
* Effect condition: until end of battle

And with this all tier 1 pets and foods are done. It should go faster for the next tiers because a lot of the mechanics have already been covered.

## Tier 2

[⬆️ Start](#start)  
[1️⃣ Tier 1](#tier-1)  
[2️⃣ Tier 2](#tier-2)  
[3️⃣ Tier 3](#tier-3)  
[4️⃣ Tier 4](#tier-4)  
[6️⃣ Tier 6](#tier-6)  
[5️⃣ Tier 5](#tier-5)  
[⬇️ Final tables](#final-tables)  
[⬇️ Rerolling shop genre](#rerolling-shop-genre)  

### Crab

{{< figure src="https://i.imgur.com/dbIBSRs.png" >}}

| Effect | Description |
| --- | --- |
| Classify | adds a class to a unit |
| Deal damage | deals damage to a unit |
| Player resource change | add, sub, mul or div of a player resource value |
| Multiple stat swap | swaps stats between multiple units |
| Push enemy | pushes an enemy to a different position |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| `Stat copy` | `copies a stat from another unit` |
| Stat set | sets a stat to a specific value |
| Summon | summons another unit |

| Effect target | Description |
| --- | --- |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| `Most healthy ally` | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N allies behind | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Dodo

{{< figure src="https://i.imgur.com/e7y7fdN.png" >}}

| Effect | Description |
| --- | --- |
| Classify | adds a class to a unit |
| Deal damage | deals damage to a unit |
| Player resource change | add, sub, mul or div of a player resource value |
| Multiple stat swap | swaps stats between multiple units |
| Push enemy | pushes an enemy to a different position |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| `Stat give` | `gives a stat to another unit` |
| Stat set | sets a stat to a specific value |
| Summon | summons another unit |

| Effect target | Description |
| --- | --- |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| Most healthy ally | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N allies behind | where N >= 1 |
| `N allies in front` | `where N >= 1` |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Elephant

{{< figure src="https://i.imgur.com/GAT9juP.png" >}}

| Trigger | Description |
| --- | --- |
| Ally summoned | when an ally is summoned |
| `Before attack` | `before the unit is about to attack` |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

| Effect | Description |
| --- | --- |
| Classify | adds a class to a unit |
| Deal damage | deals damage to a unit |
| Player resource change | add, sub, mul or div of a player resource value |
| Multiple stat swap | swaps stats between multiple units |
| Push enemy | pushes an enemy to a different position |
| `Repeat` | `repeats the effect its attached to` |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Summon | summons another unit |

The elephant is the first unit that has multiple effects. There are multiple ways of handling multiple effects, I'm personally just going to assume the simplest possible things: either the unit has multiple chains of
"trigger -> effect + condition -> target", or a single "trigger -> effect + condition -> effect + condition -> ... -> target". 
The elephant happens to be the latter, which would go like "before attack -> deal damage -> repeat -> 1 ally behind".

### Flamingo

{{< figure src="https://i.imgur.com/FgysOAq.png" >}}

* Trigger: faint
* Effect: stat change
* Effect target: 2 allies behind

Not sure if there's a difference between "faint" and "before faint", but I don't think there is.

### Hedgehog

{{< figure src="https://i.imgur.com/ctzOTsz.png" >}}

| Effect target | Description |
| --- | --- |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| `All units` | |
| Most healthy ally | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Peacock

{{< figure src="https://i.imgur.com/dTjoH7C.png" >}}

| Trigger | Description |
| --- | --- |
| Ally summoned | when an ally is summoned |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| `Hurt` | `when the unit is hit` |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

### Rat

{{< figure src="https://i.imgur.com/ZmcCjF2.png" >}}

* Trigger: faint
* Effect: summon

Technically there should be two different summon types, one for allies and one for enemies, but because summoning enemies seems kind of really specific to SAP I'm just not going to bother.

### Shrimp

{{< figure src="https://i.imgur.com/vIkzV3h.png" >}}

| Trigger | Description |
| --- | --- |
| `Ally sold` | `when an ally is sold` |
| Ally summoned | when an ally is summoned |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

### Faint

{{< figure src="https://i.imgur.com/W0ug5Qn.png" >}}

* Trigger: faint
* Effect: summon

For all summoned units the specific type of unit that is summoned is decided directly by the summon effect, since there's no real composability benefit to specifying it in any of the other tables.

### Swan

{{< figure src="https://i.imgur.com/dqSS8E5.png" >}}

* Trigger: start of turn
* Effect: player resource change

### Bat

{{< figure src="https://i.imgur.com/DNqqVwM.png" >}}

| Effect | Description |
| --- | --- |
| Classify | adds a class to a unit |
| Deal damage | deals damage to a unit |
| Player resource change | add, sub, mul or div of a player resource value |
| Multiple stat swap | swaps stats between multiple units |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| `Status effect` | `applies a status effect to a unit` |
| Summon | summons another unit |

### Dromedary

{{< figure src="https://i.imgur.com/ChWLy0z.png" >}}

* Trigger: start of turn
* Effect: stat change
* Effect target: 1st and 2nd shop units

### Tabby Cat

{{< figure src="https://i.imgur.com/icSkIuV.png" >}}

* Trigger: consumes item
* Effect: stat change
* Effect condition: until end of battle
* Effect target: all allies

| Effect target | Description |
| --- | --- |
| `All allies` | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All units | |
| Most healthy ally | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Atlantic Puffin

{{< figure src="https://i.imgur.com/RTadSG3.png" >}}

* Trigger: start of battle
* Effect: deal damage
* Effect condition: per specific ally (strawberry)
* Effect target: 1 random enemy

### Dove

{{< figure src="https://i.imgur.com/iDDRYzy.png" >}}

* Trigger: faint
* Effect: stat change
* Effect target: 2 random classed allies

### Guinea Pig

{{< figure src="https://i.imgur.com/tViSbXa.png" >}}

* Trigger: buy
* Effect: summon

### Jellyfish

{{< figure src="https://i.imgur.com/Ch8CWpw.png" >}}

| Trigger | Description |
| --- | --- |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| `Any level-up` | `when any ally levels up` |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

### Koala

{{< figure src="https://i.imgur.com/9zmMiEH.png" >}}

| Trigger | Description |
| --- | --- |
| Ally sold | when an ally is sold |
| `Ally hurt` | `when any ally is hurt` |
| Ally summoned | when an ally is summoned |
| Any level-up | when any ally levels up |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

| Effect condition | Description |
| --- | --- |
| `Limit triggers` | `applies the effect up to a max # of times per turn` |
| Per specific ally | applies the effect based on the number of allies of a specific type |
| Until the end of battle | the effect will persist until the next battle ends |

### Panda

{{< figure src="https://i.imgur.com/QncJr6q.png" >}}

* Trigger: start of battle
* Effect: give stat
* Effect target: 1 ally in front

Panda has 2 effects, the first giving its stats, and the second is fainting. This is interesting because faint is a trigger, but sometimes it's also an effect, like this in this case.
The pill can be implemented in the same way in that its effect is fainting.

| Effect | Description |
| --- | --- |
| Classify | adds a class to a unit |
| Deal damage | deals damage to a unit |
| `Faint` | `makes the unit faint` |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Summon | summons another unit |

### Pug

{{< figure src="https://i.imgur.com/aQYE6E7.png" >}}

| Effect | Description |
| --- | --- |
| Classify | adds a class to a unit |
| Deal damage | deals damage to a unit |
| Faint | makes the unit faint |
| `Give experience` | `gives experience to a unit` |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Summon | summons another unit |

### Salamander

{{< figure src="https://i.imgur.com/HPm0RFw.png" >}}

| Trigger | Description |
| --- | --- |
| `Ally bought` | `when any ally is bought` |
| Ally hurt | when any ally is hurt |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| Any level-up | when any ally levels up |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

| Effect condition | Description |
| --- | --- |
| `If specific ally` | `applies the effect if the ally passes a condition` |
| Limit triggers | applies the effect up to a max # of times per turn |
| Per specific ally | applies the effect based on the number of allies of a specific type |
| Until the end of battle | the effect will persist until the next battle ends |

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All units | |
| `Any hurt` | |
| `Any bought` | |
| Most healthy ally | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

`any hurt` and `any bought` are the more composable versions of the units that are tied with `ally hurt` and `ally bought`, like the `ally summoned` situation.

### Stork

{{< figure src="https://i.imgur.com/MfPYPap.png" >}}

* Trigger: faint
* Effect: summon

### Yak

{{< figure src="https://i.imgur.com/e5u9BIZ.png" >}}

1.
  * Trigger: end turn
  * Effect: deal damage
  * Effect target: self

2.
  * Trigger: end turn
  * Effect: stat change
  * Effect target: self

### Frigatebird

{{< figure src="https://i.imgur.com/qiwFDFx.png" >}}

* Trigger: buy
* Effect: stat change
* Effect condition: if specific ally
* Effect target: 1 random ally

### Gold Fish

{{< figure src="https://i.imgur.com/ne9kckm.png" >}}

| Effect | Description |
| --- | --- |
| Classify | adds a class to a unit |
| Deal damage | deals damage to a unit |
| `Discount` | `decreases a unit's cost` |
| Faint | makes the unit faint |
| Give experience | gives experience to a unit |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Summon | summons another unit |

### Raccoon

{{< figure src="https://i.imgur.com/B07gvzB.png" >}}

| Effect | Description |
| --- | --- |
| Classify | adds a class to a unit |
| Deal damage | deals damage to a unit |
| Discount | decreases a unit's cost |
| Faint | makes the unit faint |
| Give experience | gives experience to a unit |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| `Steal item` | `steals item from a unit` |
| Summon | summons another unit |

### Toucan

{{< figure src="https://i.imgur.com/DXOe74I.png" >}}

| Effect | Description |
| --- | --- |
| Classify | adds a class to a unit |
| Deal damage | deals damage to a unit |
| Discount | decreases a unit's cost |
| Faint | makes the unit faint |
| Give experience | gives experience to a unit |
| `Give item` | `gives your item to a unit` |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Steal item | steals item from a unit |
| Summon | summons another unit |

### Wombat

{{< figure src="https://i.imgur.com/p93dP0H.png" >}}

| Effect | Description |
| --- | --- |
| Classify | adds a class to a unit |
| `Copy ability` | `copies another unit's ability` |
| Deal damage | deals damage to a unit |
| Discount | decreases a unit's cost |
| Faint | makes the unit faint |
| Give experience | gives experience to a unit |
| Give item | gives your item to a unit |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Steal item | steals item from a unit |
| Summon | summons another unit |

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All units | |
| Any hurt | |
| Any bought | |
| `Highest tier enemy` | |
| Most healthy ally | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Cupcake

{{< figure src="https://i.imgur.com/HWSCmNr.png" >}}

* Effect: stat change
* Effect condition: until end of battle

### Meat Bone

{{< figure src="https://i.imgur.com/fSwC6G3.png" >}}

This one's a little weird, but if I were to implement it like a unit it would be something like:

* Trigger: attack
* Effect: deal damage

It's dealing extra damage on each attack, so this makes sense.

| Trigger | Description |
| --- | --- |
| Ally bought | when any ally is bought |
| Ally hurt | when any ally is hurt |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| `Attack` | `when the unit attacks` | 
| Any level-up | when any ally levels up |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

### Pill

{{< figure src="https://i.imgur.com/s3ox2cZ.png" >}}

* Effect: faint

As mentioned in the panda section.

### Broccoli

{{< figure src="https://i.imgur.com/qbO8ItK.png" >}}

* Effect: stat change

### Fried Shrimp

{{< figure src="https://i.imgur.com/zyuKNT9.png" >}}

* Effect: stat change

### Croissant

{{< figure src="https://i.imgur.com/GpBV1ND.png" >}}

* Trigger: end turn
* Effect: stat change

This is the kind of item where we have to ignore the fact that its effect can only happen while it's held.

## Tier 3

[⬆️ Start](#start)  
[1️⃣ Tier 1](#tier-1)  
[2️⃣ Tier 2](#tier-2)  
[3️⃣ Tier 3](#tier-3)  
[4️⃣ Tier 4](#tier-4)  
[6️⃣ Tier 6](#tier-6)  
[5️⃣ Tier 5](#tier-5)  
[⬇️ Final tables](#final-tables)  
[⬇️ Rerolling shop genre](#rerolling-shop-genre)  

### Badger

{{< figure src="https://i.imgur.com/w8t7fNN.png" >}}

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All units | |
| Any hurt | |
| Any bought | |
| Highest tier enemy | |
| Most healthy ally | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| `Two adjacent units` | `applies to 2 units adjacent to the one that triggered it` |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Blowfish

{{< figure src="https://i.imgur.com/QxZZ4ec.png" >}}

* Trigger: hurt
* Effect: deal damage
* Effect target: 1 random enemy

### Camel

{{< figure src="https://i.imgur.com/3nLuAW3.png" >}}

* Trigger: hurt
* Effect: stat change
* Effect target: 1 ally behind

### Dog

{{< figure src="https://i.imgur.com/Sqrn76j.png" >}}

* Trigger: ally summoned
* Effect: stat change
* Effect target: self

### Giraffe

{{< figure src="https://i.imgur.com/jmuz5hf.png" >}}

* Trigger: end turn
* EFfect: stat change
* Effect target: N allies in front

### Kangaroo

{{< figure src="https://i.imgur.com/Wtjv3dW.png" >}}

| Trigger | Description |
| --- | --- |
| `Ally ahead attacks` | `when an ally in front attacks` |
| Ally bought | when any ally is bought |
| Ally hurt | when any ally is hurt |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| Attack` | `when the unit attacks | 
| Any level-up | when any ally levels up |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

### Ox

{{< figure src="https://i.imgur.com/ErYo96O.png" >}}

| Trigger | Description |
| --- | --- |
| Ally ahead attacks | when an ally in front attacks |
| `Ally ahead faints` | `when an ally in front faints` |
| Ally bought | when any ally is bought |
| Ally hurt | when any ally is hurt |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| Attack` | `when the unit attacks | 
| Any level-up | when any ally levels up |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

| Effect | Description |
| --- | --- |
| Classify | adds a class to a unit |
| Copy ability | copies another unit's ability |
| Deal damage | deals damage to a unit |
| Discount | decreases a unit's cost |
| Faint | makes the unit faint |
| `Gain item` | `gains a specific item` |
| Give experience | gives experience to a unit |
| Give item | gives your item to a unit |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Steal item | steals item from a unit |
| Summon | summons another unit |

### Rabbit

{{< figure src="https://i.imgur.com/KGEQwkI.png" >}}

| Trigger | Description |
| --- | --- |
| Ally ahead attacks | when an ally in front attacks |
| Ally ahead faints | when an ally in front faints |
| Ally bought | when any ally is bought |
| `Ally consumes item` | `when an ally is given an item` |
| Ally hurt | when any ally is hurt |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| Attack` | `when the unit attacks | 
| Any level-up | when any ally levels up |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All units | |
| `Any that consumed item` | |
| Any hurt | |
| Any bought | |
| Highest tier enemy | |
| Most healthy ally | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Sheep

{{< figure src="https://i.imgur.com/HS4X34q.png" >}}

* Trigger: faint
* Effect: summon

### Snail

{{< figure src="https://i.imgur.com/nZCigUS.png" >}}

| Effect condition | Description |
| --- | --- |
| `If lost battle` | `applies the effect if the previous battle was lost` |
| If specific ally | applies the effect if the ally passes a condition |
| Limit triggers | applies the effect up to a max # of times per turn |
| Per specific ally | applies the effect based on the number of allies of a specific type |
| Until the end of battle | the effect will persist until the next battle ends |

### Turtle

{{< figure src="https://i.imgur.com/vmFszKI.png" >}}

* Trigger: faint
* Effect: gain item
* Effect target: N allies behind

### Hatching Chick

{{< figure src="https://i.imgur.com/7aAprel.png" >}}

1.
  * Trigger: end turn
  * Effect: stat change
  * Effect condition: until end of battle
  * Effect target: 1 ally ahead

2.
  * Trigger: end turn
  * Effect: stat change
  * Effect target: 1 ally ahead

3.
  * Trigger: start of turn
  * Effect: give experience
  * Effect target: 1 ally ahead

### Owl

{{< figure src="https://i.imgur.com/5gd3dQv.png" >}}

* Trigger: sell
* Effect: stat change
* Effect target: 1 random ally

### Puppy

{{< figure src="https://i.imgur.com/jWdFPbd.png" >}}

* Trigger: end turn
* Effect: stat gain
* Effect condition: if player resource (gold) >= 2
* Effect target: self

| Effect condition | Description |
| --- | --- |
| If lost battle | applies the effect if the previous battle was lost |
| `If player resource` | `applies the effect if a player's resource passes a condition` |
| If specific ally | applies the effect if the ally passes a condition |
| Limit triggers | applies the effect up to a max # of times per turn |
| Per specific ally | applies the effect based on the number of allies of a specific type |
| Until the end of battle | the effect will persist until the next battle ends |

### Tropical Fish

{{< figure src="https://i.imgur.com/aqNESpA.png" >}}

* Trigger: end turn
* Effect: stat change
* Effect target: two adjacent allies


### Blobfish

{{< figure src="https://i.imgur.com/BLYryY7.png" >}}

* Trigger: faint
* Effect: give experience
* Effect: stat change
* Effect target: 1 ally behind

### Capybara

{{< figure src="https://i.imgur.com/qcmrvag.png" >}}

| Trigger | Description |
| --- | --- |
| Ally ahead attacks | when an ally in front attacks |
| Ally ahead faints | when an ally in front faints |
| Ally bought | when any ally is bought |
| Ally consumes item | when an ally is given an item |
| Ally hurt | when any ally is hurt |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| Attack | when the unit attacks | 
| Any level-up | when any ally levels up |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| `Roll` | `when the shop is rerolled` |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| `All unfrozen shop units` | | 
| All units | |
| Any that consumed item | |
| Any hurt | |
| Any bought | |
| Highest tier enemy | |
| Most healthy ally | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Cassowary

{{< figure src="https://i.imgur.com/ke9qQx8.png" >}}

* Trigger: end turn
* Effect: stat change
* Effect condition: per specific ally (strawberry)
* Effect target: N random classed allies

### Clownfish

{{< figure src="https://i.imgur.com/gYD0phA.png" >}}

* Trigger: any level-up
* Effect: stat change
* Effect target: any levelled up

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| Any hurt | |
| `Any levelled up` | |
| Any that consumed item | |
| Highest tier enemy | |
| Most healthy ally | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Leech

{{< figure src="https://i.imgur.com/swpmbKr.png" >}}

1.
* Trigger: end turn
* Effect: deal damage
* Effect target: 1 ally ahead

2.
* Trigger: end turn
* Effect: stat change
* Effect target: self

### Okapi

{{< figure src="https://i.imgur.com/YvoBPU9.png" >}}

* Trigger: roll
* Effect: stat change
* Effect condition: until end of battle
* Effect condition: limit triggers
* Effect target: self

### Starfish

{{< figure src="https://i.imgur.com/hr2bT6D.png" >}}

* Trigger: ally sold
* Effect: stat change
* Effect condition: if specific ally
* Effect target: 1 random ally


### Toad

{{< figure src="https://i.imgur.com/QeLoS3a.png" >}}

* Trigger: enemy hurt
* Effect: status effect
* Effect condition: limit triggers
* Effect target: any enemy hurt

| Trigger | Description |
| --- | --- |
| Ally ahead attacks | when an ally in front attacks |
| Ally ahead faints | when an ally in front faints |
| Ally bought | when any ally is bought |
| Ally consumes item | when an ally is given an item |
| Ally hurt | when any ally is hurt |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| Attack | when the unit attacks | 
| Any level-up | when any ally levels up |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| `Enemy hurt` | `when an enemy is hurt` |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Roll | when the shop is rerolled |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| `Any enemy hurt` | |
| Any hurt | |
| Any levelled up | |
| Any that consumed item | |
| Highest tier enemy | |
| Most healthy ally | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Woodpecker

{{< figure src="https://i.imgur.com/5RNT353.png" >}}

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| Any enemy hurt | |
| Any hurt | |
| Any levelled up | |
| Any that consumed item | |
| Highest tier enemy | |
| Most healthy ally | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| `N units in front` | `where N >= 1` |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Aardvark

{{< figure src="https://i.imgur.com/d4pL5iv.png" >}}

* Trigger: enemy summoned
* Effect: stat change
* Effect target: self

### Bear

{{< figure src="https://i.imgur.com/qpvEPRh.png" >}}

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| Any enemy hurt | |
| Any hurt | |
| Any levelled up | |
| Any that consumed item | |
| Highest tier enemy | |
| Most healthy ally | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| `N adjacent units` | `where N >= 1` |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N units in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Emperor Tamarin

{{< figure src="https://i.imgur.com/DrOOV0d.png" >}}

* Trigger: sell
* Effect: stat give
* Effect target: 1st shop unit

### Seagull

{{< figure src="https://i.imgur.com/T91lYmP.png" >}}

| Effect | Description |
| --- | --- |
| Classify | adds a class to a unit |
| Copy ability | copies another unit's ability |
| `Copy item to` | `copies this unit's item to another unit` |
| Deal damage | deals damage to a unit |
| Discount | decreases a unit's cost |
| Faint | makes the unit faint |
| Gain item | gains a specific item |
| Give experience | gives experience to a unit |
| Give item | gives your item to a unit |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Steal item | steals item from a unit |
| Summon | summons another unit |

### Wasp

{{< figure src="https://i.imgur.com/kBz3DI8.png" >}}

* Trigger: upgrade shop tier
* Effect: stat change
* Effect target: self

### Garlic

{{< figure src="https://i.imgur.com/jAAmIFC.png" >}}

Like the meat bone, you could describe this in terms of its trigger and effect. I would do it like this:

* Trigger: hurt
* Effect: take less damage

So whenever this unit takes damage, it will take less damage.

| Effect | Description |
| --- | --- |
| Classify | adds a class to a unit |
| Copy ability | copies another unit's ability |
| Copy item to | copies this unit's item to another unit |
| Deal damage | deals damage to a unit |
| Discount | decreases a unit's cost |
| Faint | makes the unit faint |
| Gain item | gains a specific item |
| Give experience | gives experience to a unit |
| Give item | gives your item to a unit |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Steal item | steals item from a unit |
| Summon | summons another unit |
| `Take less damage` | `takes less damage from the next attack` |

### Salad Bowl

{{< figure src="https://i.imgur.com/7k89sjB.png" >}}

* Effect: stat change
* Effect target: 2 random allies

### Cucumber

{{< figure src="https://i.imgur.com/Qz96Zkw.png" >}}

* Trigger: end turn
* Effect: stat change

### Lollipop

{{< figure src="https://i.imgur.com/I4uDVAF.png" >}}

| Effect | Description |
| --- | --- |
| Classify | adds a class to a unit |
| Copy ability | copies another unit's ability |
| Copy item to | copies this unit's item to another unit |
| Deal damage | deals damage to a unit |
| Discount | decreases a unit's cost |
| Faint | makes the unit faint |
| Gain item | gains a specific item |
| Give experience | gives experience to a unit |
| Give item | gives your item to a unit |
| `Single stat swap` | `swaps stats within a unit` |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Steal item | steals item from a unit |
| Summon | summons another unit |
| Take less damage | takes less damage from the next attack |

### Pineapple

{{< figure src="https://i.imgur.com/WBsGxTY.png" >}}

This is essentially dealing more damage when the ability deals damage, so something like:

* Trigger: ability damage
* Effect: deal damage

| Trigger | Description |
| --- | --- |
| `Ability damage` | `when the unit's ability deals damage` |
| Ally ahead attacks | when an ally in front attacks |
| Ally ahead faints | when an ally in front faints |
| Ally bought | when any ally is bought |
| Ally consumes item | when an ally is given an item |
| Ally hurt | when any ally is hurt |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| Attack | when the unit attacks | 
| Any level-up | when any ally levels up |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy hurt | when an enemy is hurt |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Roll | when the shop is rerolled |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

## Tier 4

[⬆️ Start](#start)  
[1️⃣ Tier 1](#tier-1)  
[2️⃣ Tier 2](#tier-2)  
[3️⃣ Tier 3](#tier-3)  
[4️⃣ Tier 4](#tier-4)  
[6️⃣ Tier 6](#tier-6)  
[5️⃣ Tier 5](#tier-5)  
[⬇️ Final tables](#final-tables)  
[⬇️ Rerolling shop genre](#rerolling-shop-genre)  

### Bison

{{< figure src="https://i.imgur.com/TFzkPOG.png" >}}

| Effect condition | Description |
| --- | --- |
| `If any specific ally` | `applies the effect if at least one ally passes a condition` |
| If lost battle | applies the effect if the previous battle was lost |
| If player resource | applies the effect if a player's resource passes a condition |
| If specific ally | applies the effect if the ally passes a condition |
| Limit triggers | applies the effect up to a max # of times per turn |
| Per specific ally | applies the effect based on the number of allies of a specific type |
| Until the end of battle | the effect will persist until the next battle ends |

### Deer

{{< figure src="https://i.imgur.com/PZIil1l.png" >}}

* Trigger: faint
* Effect: summon

### Dolphin

{{< figure src="https://i.imgur.com/5RjZkd0.png" >}}

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| Any enemy hurt | |
| Any hurt | |
| Any levelled up | |
| Any that consumed item | |
| Highest tier enemy | |
| `Least healthy ally` | |
| Most healthy ally | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N adjacent units | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N units in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| Self | applies to the unit that triggered it |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Hippo

{{< figure src="https://i.imgur.com/vSC9p3G.png" >}}

| Trigger | Description |
| --- | --- |
| Ability damage | when the unit's ability deals damage |
| Ally ahead attacks | when an ally in front attacks |
| Ally ahead faints | when an ally in front faints |
| Ally bought | when any ally is bought |
| Ally consumes item | when an ally is given an item |
| Ally hurt | when any ally is hurt |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| Attack | when the unit attacks | 
| Any level-up | when any ally levels up |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy hurt | when an enemy is hurt |
| `Enemy killed` | `when the enemy is killed as a result of this unit's attack` |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Roll | when the shop is rerolled |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

### Parrot

{{< figure src="https://i.imgur.com/OeFAMNH.png" >}}

* Trigger: end turn
* Effect: copy ability
* Effect condition: until end of battle
* Effect target: 1 friend ahead

### Penguin

{{< figure src="https://i.imgur.com/7PCtiZu.png" >}}

* Trigger: end turn
* Effect: stat change
* Effect condition: if specific ally
* Effect target: 3 specific allies

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| Any enemy hurt | |
| Any hurt | |
| Any levelled up | |
| Any that consumed item | |
| Highest tier enemy | |
| Least healthy ally | |
| Most healthy ally | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N adjacent units | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N units in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| `N specific allies` | `where N >= 1, ally specified in effect condition` |
| Self | applies to the unit that triggered it |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Rooster

{{< figure src="https://i.imgur.com/HjIaCMg.png" >}}

* Trigger: faint
* Effect: summon

### Skunk

{{< figure src="https://i.imgur.com/4vrWp1Y.png" >}}

* Trigger: start of battle
* Effect: stat change
* Effect target: most healthy enemy

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| Any enemy hurt | |
| Any hurt | |
| Any levelled up | |
| Any that consumed item | |
| Highest tier enemy | |
| Least healthy ally | |
| Most healthy ally | |
| `Most healthy enemy` | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N adjacent units | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N units in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| N specific allies | where N >= 1, ally specified in effect condition |
| Self | applies to the unit that triggered it |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Squirrel

{{< figure src="https://i.imgur.com/rMHzeQd.png" >}}

| Effect | Description |
| --- | --- |
| `Add shop item` | `adds an additional item to the shop` |
| Classify | adds a class to a unit |
| Copy ability | copies another unit's ability |
| Copy item to | copies this unit's item to another unit |
| Deal damage | deals damage to a unit |
| Discount unit | decreases a shop unit's cost |
| `Discount item` | `decreases a shop item's cost` |
| Faint | makes the unit faint |
| Gain item | gains a specific item |
| Give experience | gives experience to a unit |
| Give item | gives your item to a unit |
| Single stat swap | swaps stats within a unit |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Steal item | steals item from a unit |
| Summon | summons another unit |
| Take less damage | takes less damage from the next attack |

### Whale

{{< figure src="https://i.imgur.com/KCgvgii.png" >}}

1.
* Trigger: start of battle
* Effect: faint
* Effect target: 1 friend ahead

2.
* Trigger: faint
* Effect: summon

This is a weird one because it has to store the unit it kills. I could try to encapsulate that into a composable mechanic, like "copy unit", but I think it's best to just go for something simpler
like "summon", which would summon a specific unit, and then that specific unit is specified to be the one it killed at a lower level of abstraction.

### Worm

{{< figure src="https://i.imgur.com/ctHStPq.png" >}}

* Trigger: consumes item
* Effect: stat change
* Effect target: self

### Buffalo

{{< figure src="https://i.imgur.com/Mm8dNbC.png" >}}

* Trigger: ally bought
* Effect: stat change
* Effect condition: limit triggers
* Effect target: self

### Caterpillar

{{< figure src="https://i.imgur.com/UFwAkdt.png" >}}

1.
* Trigger: start of turn
* Effect: give experience
* Effect target: self

2.
* Trigger: start of battle
* Effect: transform
* Effect target: self

3.
* Trigger: start of battle
* Effect: stat copy
* Effect target: strongest ally

| Effect | Description |
| --- | --- |
| Add shop item | adds an additional item to the shop |
| Classify | adds a class to a unit |
| Copy ability | copies another unit's ability |
| Copy item to | copies this unit's item to another unit |
| Deal damage | deals damage to a unit |
| Discount unit | decreases a shop unit's cost |
| Discount item | decreases a shop item's cost |
| Faint | makes the unit faint |
| Gain item | gains a specific item |
| Give experience | gives experience to a unit |
| Give item | gives your item to a unit |
| Single stat swap | swaps stats within a unit |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Steal item | steals item from a unit |
| Summon | summons another unit |
| Take less damage | takes less damage from the next attack |
| `Transform` | `transforms into another unit` |

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| Any enemy hurt | |
| Any hurt | |
| Any levelled up | |
| Any that consumed item | |
| Highest tier enemy | |
| Least healthy ally | |
| Most healthy ally | |
| Most healthy enemy | |
| Nth ally | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N adjacent units | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N units in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| N specific allies | where N >= 1, ally specified in effect condition |
| Self | applies to the unit that triggered it |
| `Strongest ally` | |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Llama

{{< figure src="https://i.imgur.com/MbRYS6X.png" >}}

* Trigger: end turn
* Effect: stat change
* Effect condition: if player resource (number of pets) <= 4
* Effect target: self

### Lobster

{{< figure src="https://i.imgur.com/AggOv2p.png" >}}

* Trigger: ally summoned
* Effect: stat change
* Effect target: any ally summoned

### Microbe

{{< figure src="https://i.imgur.com/11kJS3P.png" >}}

* Trigger: faint
* Effect: status effect
* Effect target: all units

### Anteater

{{< figure src="https://i.imgur.com/pNj5jOG.png" >}}

* Trigger: faint
* Effect: summon


### Crow

{{< figure src="https://i.imgur.com/MJf0Bxt.png" >}}

* Trigger: sell
* Effect: replace shop item

### Donkey


{{< figure src="https://i.imgur.com/ncj27UD.png" >}}

* Trigger: ally faints
* Effect: push enemy
* Effect target: 5th enemy

| Trigger | Description |
| --- | --- |
| Ability damage | when the unit's ability deals damage |
| Ally ahead attacks | when an ally in front attacks |
| Ally ahead faints | when an ally in front faints |
| Ally bought | when any ally is bought |
| Ally consumes item | when an ally is given an item |
| `Ally faints` | `when an ally faints` |
| Ally hurt | when any ally is hurt |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| Attack | when the unit attacks | 
| Any level-up | when any ally levels up |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy hurt | when an enemy is hurt |
| Enemy killed | when the enemy is killed as a result of this unit's attack |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Roll | when the shop is rerolled |
| Sell | when the unit is sold |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| Any enemy hurt | |
| Any hurt | |
| Any levelled up | |
| Any that consumed item | |
| Highest tier enemy | |
| Least healthy ally | |
| Most healthy ally | |
| Most healthy enemy | |
| Nth ally | where N >= 1 |
| `Nth enemy` | `where N >= 1` |
| Nth shop unit | where N >= 1 |
| N adjacent units | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N units in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| N specific allies | where N >= 1, ally specified in effect condition |
| Self | applies to the unit that triggered it |
| Strongest ally | |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Eel

{{< figure src="https://i.imgur.com/yhQWbtR.png" >}}

* Trigger: start of battle
* Effect: stat change
* Effect target: self

### Hawk

{{< figure src="https://i.imgur.com/ZuLQBVW.png" >}}

* Trigger: start of battle
* Effect: deal damage
* Effect target: Nth enemy, where N = this unit's position

### Orangutan

{{< figure src="https://i.imgur.com/7NwfehL.png" >}}

* Trigger: end turn
* Effect: stat change
* Effect target: least healthy ally

### Pelican

{{< figure src="https://i.imgur.com/NO4MSG1.png" >}}

* Trigger: end turn, start of battle
* Effect: stat change
* Effect condition: if specific ally
* Effect target: random classed ally

### Platypus

{{< figure src="https://i.imgur.com/GaTnUQ8.png" >}}

* Trigger: sell
* Effect: summon

### Praying Mantis

{{< figure src="https://i.imgur.com/SNUeYk4.png" >}}

1. 
* Trigger: start of turn
* Effect: kill
* Effect target: two adjacent allies

2.
* Trigger: start of turn
* Effect: stat change
* Effect target: self

| Effect | Description |
| --- | --- |
| Add shop item | adds an additional item to the shop |
| Classify | adds a class to a unit |
| Copy ability | copies another unit's ability |
| Copy item to | copies this unit's item to another unit |
| Deal damage | deals damage to a unit |
| Discount unit | decreases a shop unit's cost |
| Discount item | decreases a shop item's cost |
| Faint | makes the unit faint |
| Gain item | gains a specific item |
| Give experience | gives experience to a unit |
| Give item | gives your item to a unit |
| `Kill` | `deals damage and kill a unit` |
| Single stat swap | swaps stats within a unit |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Steal item | steals item from a unit |
| Summon | summons another unit |
| Take less damage | takes less damage from the next attack |
| Transform | transforms into another unit |

### Armadillo 

{{< figure src="https://i.imgur.com/o16XKWB.png" >}}

* Trigger: hurt, faint
* Effect: stat change
* Effect target: all allies

### Dragonfly

{{< figure src="https://i.imgur.com/IiJFnTl.png" >}}

* Trigger: end turn
* Effect: stat change
* Effect target: 1 random ally of each level

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| Any enemy hurt | |
| Any hurt | |
| Any levelled up | |
| Any that consumed item | |
| Highest tier enemy | |
| Least healthy ally | |
| Most healthy ally | |
| Most healthy enemy | |
| Nth ally | where N >= 1 |
| Nth enemy | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N adjacent units | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N units in front | where N >= 1 |
| N random allies | where N >= 1 |
| `N random allies of each level` | `where N >= 1` |
| `N random allies of each tier ` | `where N >= 1` |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| N specific allies | where N >= 1, ally specified in effect condition |
| Self | applies to the unit that triggered it |
| Strongest ally | |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Jerboa

{{< figure src="https://i.imgur.com/WbA3b4W.png" >}}

* Trigger: consumes item
* Effect: stat change
* Effect target: all allies

### Lynx

{{< figure src="https://i.imgur.com/Fn0yIoG.png" >}}

* Trigger: start of battle
* Effect: deal damage
* Effect target: 1 random enemy

### Mole

{{< figure src="https://i.imgur.com/rKNwCCq.png" >}}

* Trigger: buy
* Effect: stat change
* Effect target: two adjacent allies

### Porcupine

{{< figure src="https://i.imgur.com/QHcRlKh.png" >}}

* Trigger: hurt
* Effect: deal damage
* Effect target: attacking enemy

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| Any enemy hurt | |
| Any hurt | |
| Any levelled up | |
| Any that consumed item | |
| `Attacking enemy` | `the enemy that just attacked this unit` |
| Highest tier enemy | |
| Least healthy ally | |
| Most healthy ally | |
| Most healthy enemy | |
| Nth ally | where N >= 1 |
| Nth enemy | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N adjacent units | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N units in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random allies of each level | where N >= 1 |
| N random allies of each tier | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| N specific allies | where N >= 1, ally specified in effect condition |
| Self | applies to the unit that triggered it |
| Strongest ally | |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Canned Food

{{< figure src="https://i.imgur.com/TAPBXKm.png" >}}

* Effect: stat change
* Effect target: all shop units
* Effect target: all future shop units

| Effect target | Description |
| --- | --- |
| All allies | |
| All shop units | |
| `All future shop units` | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| Any enemy hurt | |
| Any hurt | |
| Any levelled up | |
| Any that consumed item | |
| Attacking enemy | the enemy that just attacked this unit |
| Highest tier enemy | |
| Least healthy ally | |
| Most healthy ally | |
| Most healthy enemy | |
| Nth ally | where N >= 1 |
| Nth enemy | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N adjacent units | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N units in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random allies of each level | where N >= 1 |
| N random allies of each tier | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| N specific allies | where N >= 1, ally specified in effect condition |
| Self | applies to the unit that triggered it |
| Strongest ally | |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Pear

{{< figure src="https://i.imgur.com/nWQVSdM.png" >}}

* Effect: stat change

### Cheese

{{< figure src="https://i.imgur.com/6zm6hHZ.png" >}}

* Trigger: attack
* Effect: double damage (100%)
* Effect: remove item

| Effect | Description |
| --- | --- |
| Add shop item | adds an additional item to the shop |
| Classify | adds a class to a unit |
| Copy ability | copies another unit's ability |
| Copy item to | copies this unit's item to another unit |
| Deal damage | deals damage to a unit |
| `Double damage` | `chance to deal double damage to a unit` |
| Discount unit | decreases a shop unit's cost |
| Discount item | decreases a shop item's cost |
| Faint | makes the unit faint |
| Gain item | gains a specific item |
| Give experience | gives experience to a unit |
| Give item | gives your item to a unit |
| Kill | deals damage and kill a unit |
| Single stat swap | swaps stats within a unit |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| `Remove item` | `removes this unit's held item` |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Steal item | steals item from a unit |
| Summon | summons another unit |
| Take less damage | takes less damage from the next attack |
| Transform | transforms into another unit |

### Grapes

{{< figure src="https://i.imgur.com/nbsd4Gf.png" >}}

* Trigger: start of turn
* Effect: player resource change

### Fortune Cookie

{{< figure src="https://i.imgur.com/0S5SImX.png" >}}

* Trigger: attack
* Effect: double damage (50%)

## Tier 6

[⬆️ Start](#start)  
[1️⃣ Tier 1](#tier-1)  
[2️⃣ Tier 2](#tier-2)  
[3️⃣ Tier 3](#tier-3)  
[4️⃣ Tier 4](#tier-4)  
[6️⃣ Tier 6](#tier-6)  
[5️⃣ Tier 5](#tier-5)  
[⬇️ Final tables](#final-tables)  
[⬇️ Rerolling shop genre](#rerolling-shop-genre)  

### Boar

{{< figure src="https://i.imgur.com/vmPADd3.png" >}}

* Trigger: before attack
* Effect: stat change
* Effect target: self

### Cat

{{< figure src="https://i.imgur.com/41r4N5D.png" >}}

| Effect | Description |
| --- | --- |
| Add shop item | adds an additional item to the shop |
| Classify | adds a class to a unit |
| Copy ability | copies another unit's ability |
| Copy item to | copies this unit's item to another unit |
| Deal damage | deals damage to a unit |
| Double damage | chance to deal double damage to a unit |
| Discount unit | decreases a shop unit's cost |
| Discount item | decreases a shop item's cost |
| Faint | makes the unit faint |
| Gain item | gains a specific item |
| Give experience | gives experience to a unit |
| Give item | gives your item to a unit |
| `Item effectiveness` | `add, sub, mul or div to item effectiveness` |
| Kill | deals damage and kill a unit |
| Single stat swap | swaps stats within a unit |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Remove item | removes this unit's held item |
| Roll shop | rolls the shop |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Steal item | steals item from a unit |
| Summon | summons another unit |
| Take less damage | takes less damage from the next attack |
| Transform | transforms into another unit |

### Dragon

{{< figure src="https://i.imgur.com/5D700LF.png" >}}

| Trigger | Description |
| --- | --- |
| Ability damage | when the unit's ability deals damage |
| Ally ahead attacks | when an ally in front attacks |
| Ally ahead faints | when an ally in front faints |
| Ally bought | when any ally is bought |
| Ally consumes item | when an ally is given an item |
| Ally faints | when an ally faints |
| Ally hurt | when any ally is hurt |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| Attack | when the unit attacks | 
| Any level-up | when any ally levels up |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy hurt | when an enemy is hurt |
| Enemy killed | when the enemy is killed as a result of this unit's attack |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Roll | when the shop is rerolled |
| Sell | when the unit is sold |
| `Specific ally bought` | `when a specific ally or type of ally is bought` |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

### Fly

{{< figure src="https://i.imgur.com/O5ukJzy.png" >}}

* Trigger: ally faints
* Effect: summon
* Effect condition: limit triggers

### Gorilla

{{< figure src="https://i.imgur.com/5szdK8a.png" >}}

* Trigger: hurt
* Effect: give item
* Effect condition: limit triggers
* Effect target: self

### Leopard

{{< figure src="https://i.imgur.com/t1iyku4.png" >}}

* Trigger: start of battle
* Effect: deal damage
* Effect target: 1 random enemy

### Mammoth

{{< figure src="https://i.imgur.com/rgt1Q7Y.png" >}}

* Trigger: faint
* Effect: stat change
* Effect target: all allies

### Snake

{{< figure src="https://i.imgur.com/A1NBTwa.png" >}}

* Trigger: ally ahead attacks
* Effect: deal damage
* Effect target: 1 random enemy

### Tiger

{{< figure src="https://i.imgur.com/7wQonHJ.png" >}}

* Trigger: ally ahead uses ability
* Effect: repeat

The tiger makes another unit repeat their ability, which makes representing it in this system kind of awkward. Still, "ally ahead uses ability" is a fairly composable trigger so it should be added.

| Trigger | Description |
| --- | --- |
| Ability damage | when the unit's ability deals damage |
| Ally ahead attacks | when an ally in front attacks |
| Ally ahead faints | when an ally in front faints |
| `Ally ahead uses ability` | `when an ally in front uses its ability` |
| Ally bought | when any ally is bought |
| Ally consumes item | when an ally is given an item |
| Ally faints | when an ally faints |
| Ally hurt | when any ally is hurt |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| Attack | when the unit attacks | 
| Any level-up | when any ally levels up |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy hurt | when an enemy is hurt |
| Enemy killed | when the enemy is killed as a result of this unit's attack |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Roll | when the shop is rerolled |
| Sell | when the unit is sold |
| Specific ally bought | when a specific ally or type of ally is bought |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

### Octopus

{{< figure src="https://i.imgur.com/vsw4JL7.png" >}}

* Trigger: before attack
* Effect: deal damage
* Effect target: 2 random enemies

### Sauropod

{{< figure src="https://i.imgur.com/O14lelA.png" >}}

* Trigger: item bought
* Effect: player resource change
* Effect condition: limit triggers

### Tyrannosaurus

{{< figure src="https://i.imgur.com/0phsdAs.png" >}}

* Trigger: end turn
* Effect: stat change
* Effect condition: if player resource (gold) >= 3
* Effect target: all allies

### Hammershark

{{< figure src="https://i.imgur.com/v2cheAi.png" >}}

* Trigger: start of turn
* Effect: player resource change
* Effect condition: if any specific ally

### Komodo

{{< figure src="https://i.imgur.com/tJLBH0p.png" >}}

* Trigger: end turn
* Effect: stat change
* Effect: shuffle
* Effect target: all allies ahead

| Effect | Description |
| --- | --- |
| Add shop item | adds an additional item to the shop |
| Classify | adds a class to a unit |
| Copy ability | copies another unit's ability |
| Copy item to | copies this unit's item to another unit |
| Deal damage | deals damage to a unit |
| Double damage | chance to deal double damage to a unit |
| Discount unit | decreases a shop unit's cost |
| Discount item | decreases a shop item's cost |
| Faint | makes the unit faint |
| Gain item | gains a specific item |
| Give experience | gives experience to a unit |
| Give item | gives your item to a unit |
| Item effectiveness | add, sub, mul or div to item effectiveness |
| Kill | deals damage and kill a unit |
| Single stat swap | swaps stats within a unit |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Remove item | removes this unit's held item |
| Roll shop | rolls the shop |
| `Shuffle` | `changes the positions of multiple units` |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Steal item | steals item from a unit |
| Summon | summons another unit |
| Take less damage | takes less damage from the next attack |
| Transform | transforms into another unit |

| Effect target | Description |
| --- | --- |
| All allies | |
| `All allies ahead` | |
| All shop units | |
| All future shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| Any enemy hurt | |
| Any hurt | |
| Any levelled up | |
| Any that consumed item | |
| Attacking enemy | the enemy that just attacked this unit |
| Highest tier enemy | |
| Least healthy ally | |
| Most healthy ally | |
| Most healthy enemy | |
| Nth ally | where N >= 1 |
| Nth enemy | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N adjacent units | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N units in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random allies of each level | where N >= 1 |
| N random allies of each tier | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| N specific allies | where N >= 1, ally specified in effect condition |
| Self | applies to the unit that triggered it |
| Strongest ally | |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Orca

{{< figure src="https://i.imgur.com/wKZ1n2G.png" >}}

* Trigger: faint
* Effect: summon

### Ostrich

{{< figure src="https://i.imgur.com/l8dTV9j.png" >}}

* Trigger: end turn
* Effect: stat change
* Effect condition: per specific ally
* Effect target: self

### Piranha

{{< figure src="https://i.imgur.com/QF8agpi.png" >}}

* Trigger: hurt, faint
* Effect: stat change
* Effect target: all allies

### Reindeer

{{< figure src="https://i.imgur.com/gPYF1ll.png" >}}

* Trigger: before attack
* Effect: give item
* Effect condition: limit triggers
* Effect target: self

### Sabertooth Tiger

{{< figure src="https://i.imgur.com/cJxjidT.png" >}}

* Trigger: hurt
* Effect: summon

### Spinosaurus

{{< figure src="https://i.imgur.com/1bItNgA.png" >}}

* Trigger: ally faints
* Effect: stat change
* Effect target: 1 random ally

### Stegosaurus

{{< figure src="https://i.imgur.com/dfhDvpI.png" >}}

* Trigger: end turn
* Effect: stat change
* Effect condition: until end of battle
* Effect condition: per turn number
* Effect target: 1 ally ahead

| Effect condition | Description |
| --- | --- |
| If any specific ally | applies the effect if at least one ally passes a condition |
| If lost battle | applies the effect if the previous battle was lost |
| If player resource | applies the effect if a player's resource passes a condition |
| If specific ally | applies the effect if the ally passes a condition |
| Limit triggers | applies the effect up to a max # of times per turn |
| `Per turn number` | `applies the effect based on the number of turns` |
| Per specific ally | applies the effect based on the number of allies of a specific type |
| Until the end of battle | the effect will persist until the next battle ends |

### Velociraptor

{{< figure src="https://i.imgur.com/BT6sYpE.png" >}}

* Trigger: start of battle
* Effect: give item
* Effect target: 1 random classed ally

### Alpaca

{{< figure src="https://i.imgur.com/lmQYW51.png" >}}

* Trigger: ally summoned
* Effect: give experience
* Effect condition: limit triggers
* Effect target: any summoned ally

### Lioness

{{< figure src="https://i.imgur.com/mgUCCMm.png" >}}

* Trigger: end turn
* Effect: stat change
* Effect target: all shop units, all future shop units

### Tapir

{{< figure src="https://i.imgur.com/jpicriE.png" >}}

* Trigger: faint
* Effect: summon

### Walrus

{{< figure src="https://i.imgur.com/hkFUz2g.png" >}}

* Trigger: faint
* Effect: give item
* Effect target: N random allies

### White Tiger

{{< figure src="https://i.imgur.com/3BgLidb.png" >}}

* Trigger: start of battle
* Effect: set level
* Effect target: N allies behind 

| Effect | Description |
| --- | --- |
| Add shop item | adds an additional item to the shop |
| Classify | adds a class to a unit |
| Copy ability | copies another unit's ability |
| Copy item to | copies this unit's item to another unit |
| Deal damage | deals damage to a unit |
| Double damage | chance to deal double damage to a unit |
| Discount unit | decreases a shop unit's cost |
| Discount item | decreases a shop item's cost |
| Faint | makes the unit faint |
| Gain item | gains a specific item |
| Give experience | gives experience to a unit |
| Give item | gives your item to a unit |
| Item effectiveness | add, sub, mul or div to item effectiveness |
| Kill | deals damage and kill a unit |
| Single stat swap | swaps stats within a unit |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Remove item | removes this unit's held item |
| Roll shop | rolls the shop |
| `Set level` | `sets the unit's level to a specific value` |
| Shuffle | changes the positions of multiple units |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Steal item | steals item from a unit |
| Summon | summons another unit |
| Take less damage | takes less damage from the next attack |
| Transform | transforms into another unit |

### Melon

{{< figure src="https://i.imgur.com/3uuwPcf.png" >}}

* Trigger: damage taken
* Effect: take less damage
* Effect: remove item

| Trigger | Description |
| --- | --- |
| Ability damage | when the unit's ability deals damage |
| Ally ahead attacks | when an ally in front attacks |
| Ally ahead faints | when an ally in front faints |
| Ally ahead uses ability | when an ally in front uses its ability |
| Ally bought | when any ally is bought |
| Ally consumes item | when an ally is given an item |
| Ally faints | when an ally faints |
| Ally hurt | when any ally is hurt |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| Attack | when the unit attacks | 
| Any level-up | when any ally levels up |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| `Damage taken` | `when the unit takes damage` |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy hurt | when an enemy is hurt |
| Enemy killed | when the enemy is killed as a result of this unit's attack |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Roll | when the shop is rerolled |
| Sell | when the unit is sold |
| Specific ally bought | when a specific ally or type of ally is bought |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Upgrade shop tier | when the shop levels up |

### Mushroom

{{< figure src="https://i.imgur.com/Goqt1bT.png" >}}

* Trigger: faint
* Effect: summon

### Pizza

{{< figure src="https://i.imgur.com/uRezA0D.png" >}}

* Effect: stat change
* Effect target: 2 random allies

### Steak

{{< figure src="https://i.imgur.com/wjhloxX.png" >}}

* Trigger: attack
* Effect: deal damage
* Effect: remove item

### Hot Dog

{{< figure src="https://i.imgur.com/0cmlJKu.png" >}}

* Effect: stat change
* Effect target: 2 random allies

### Orange

{{< figure src="https://i.imgur.com/JyHcNv2.png" >}}

* Effect: stat change
* Effect target: 2 random allies

### Popcorn

{{< figure src="https://i.imgur.com/JlHaJmV.png" >}}

* Trigger: faint
* Effect: summon

### Chicken Leg

{{< figure src="https://i.imgur.com/UKCC9Lq.png" >}}

* Effect: stat change

### Soft Ice

{{< figure src="https://i.imgur.com/uCPvsU3.png" >}}

* Effect: stat change
* Effect target: all allies

## Tier 5

[⬆️ Start](#start)  
[1️⃣ Tier 1](#tier-1)  
[2️⃣ Tier 2](#tier-2)  
[3️⃣ Tier 3](#tier-3)  
[4️⃣ Tier 4](#tier-4)  
[6️⃣ Tier 6](#tier-6)  
[5️⃣ Tier 5](#tier-5)  
[⬇️ Final tables](#final-tables)  
[⬇️ Rerolling shop genre](#rerolling-shop-genre)  

By mistake I did tier 6 before tier 5, but the order doesn't matter so I can't be bothered to fix it.

### Cow

{{< figure src="https://i.imgur.com/1HivWCB.png" >}}

* Trigger: buy
* Effect: replace item

### Crocodile

{{< figure src="https://i.imgur.com/0Q3qMfB.png" >}}

* Trigger: start of battle
* Effect: deal damage
* Effect: repeat
* Effect target: 5th enemy

### Monkey

{{< figure src="https://i.imgur.com/UxqrhC0.png" >}}

* Trigger: end turn
* Effect: stat change
* Effect target: 1st ally

### Rhino

{{< figure src="https://i.imgur.com/HcxWZx0.png" >}}

* Trigger: enemy killed
* Effect: deal damage
* Effect target: 1st enemy

### Scorpion

{{< figure src="https://i.imgur.com/t6ifbm4.png" >}}

* Trigger: summoned
* Effect: give item
* Effect target: self

| Trigger | Description |
| --- | --- |
| Ability damage | when the unit's ability deals damage |
| Ally ahead attacks | when an ally in front attacks |
| Ally ahead faints | when an ally in front faints |
| Ally ahead uses ability | when an ally in front uses its ability |
| Ally bought | when any ally is bought |
| Ally consumes item | when an ally is given an item |
| Ally faints | when an ally faints |
| Ally hurt | when any ally is hurt |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| Attack | when the unit attacks | 
| Any level-up | when any ally levels up |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| Damage taken | when the unit takes damage |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy hurt | when an enemy is hurt |
| Enemy killed | when the enemy is killed as a result of this unit's attack |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Roll | when the shop is rerolled |
| Sell | when the unit is sold |
| Specific ally bought | when a specific ally or type of ally is bought |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| `Summoned` | `when this unit is summoned` |
| Upgrade shop tier | when the shop levels up |

### Seal

{{< figure src="https://i.imgur.com/e4hm0lE.png" >}}

* Trigger: consumes item
* Effect: stat change
* Effect target: 2 random allies

### Shark

{{< figure src="https://i.imgur.com/4dbdDB6.png" >}}

* Trigger: ally faints
* Effect: stat change
* Effect target: self

### Turkey

{{< figure src="https://i.imgur.com/v5P8Va1.png" >}}

* Trigger: ally summoned
* Effect: stat change
* Effect target: any summoned ally

### Chicken

{{< figure src="https://i.imgur.com/PPq48dB.png" >}}

* Trigger: specific ally bought
* Effect: stat change
* Effect target: all shop units, all future shop units

### Eagle

{{< figure src="https://i.imgur.com/iK8cGGS.png" >}}

* Trigger: faint
* Effect: summon

### Goat

{{< figure src="https://i.imgur.com/IgWfprT.png" >}}

* Trigger: ally bought
* Effect: player resource change
* Effect condition: limit triggers

### Poodle

{{< figure src="https://i.imgur.com/w5vIwud.png" >}}

* Trigger: end turn
* Effect: stat change
* Effect target: 1 random ally of each tier

### Fox

{{< figure src="https://i.imgur.com/Ugfz4Yq.png" >}}

1.
* Trigger: end turn
* Effect: steal item

2. 
* Trigger: end turn
* Effect: steal item
* Effect: item effectiveness

### Hamster

{{< figure src="https://i.imgur.com/1siPamA.png" >}}

* Trigger: roll
* Effect: player resource change
* Effect condition: limit triggers

### Lion

{{< figure src="https://i.imgur.com/6CorxBC.png" >}}

* Trigger: start of battle
* Effect: stat change
* Effect condition: if highest tier ally
* Effect target: self

| Effect condition | Description |
| --- | --- |
| If any specific ally | applies the effect if at least one ally passes a condition |
| `If highest tier ally` | `applies the effect if this is the highest tier unit` |
| If lost battle | applies the effect if the previous battle was lost |
| If player resource | applies the effect if a player's resource passes a condition |
| If specific ally | applies the effect if the ally passes a condition |
| Limit triggers | applies the effect up to a max # of times per turn |
| Per turn number | applies the effect based on the number of turns |
| Per specific ally | applies the effect based on the number of allies of a specific type |
| Until the end of battle | the effect will persist until the next battle ends |

### Polar Bear

{{< figure src="https://i.imgur.com/kH3KOOC.png" >}}

* Trigger: start of turn
* Effect: stat change
* Effect target: 1 random frozen shop unit

| Effect target | Description |
| --- | --- |
| All allies | |
| All allies ahead | |
| All shop units | |
| All future shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| Any enemy hurt | |
| Any hurt | |
| Any levelled up | |
| Any that consumed item | |
| Attacking enemy | the enemy that just attacked this unit |
| Highest tier enemy | |
| Least healthy ally | |
| Most healthy ally | |
| Most healthy enemy | |
| Nth ally | where N >= 1 |
| Nth enemy | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N adjacent units | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N units in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random allies of each level | where N >= 1 |
| N random allies of each tier | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| `N random frozen shop units` | `where N >= 1` |
| N specific allies | where N >= 1, ally specified in effect condition |
| Self | applies to the unit that triggered it |
| Strongest ally | |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Shoebill

{{< figure src="https://i.imgur.com/TFTecQP.png" >}}

* Trigger: end turn
* Effect: stat change
* Effect target: all classed allies

### Siberian Husky

{{< figure src="https://i.imgur.com/4IPCbHr.png" >}}

* Trigger: end turn
* Effect: stat change
* EFfect target: all specific allies

| Effect target | Description |
| --- | --- |
| All allies | |
| All allies ahead | |
| `All classed allies` | `classed ally = of a specific class` |
| `All specific allies` | `specific ally = ally that passes a specific condition` |
| All shop units | |
| All future shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| Any enemy hurt | |
| Any hurt | |
| Any levelled up | |
| Any that consumed item | |
| Attacking enemy | the enemy that just attacked this unit |
| Highest tier enemy | |
| Least healthy ally | |
| Most healthy ally | |
| Most healthy enemy | |
| Nth ally | where N >= 1 |
| Nth enemy | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N adjacent units | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N units in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random allies of each level | where N >= 1 |
| N random allies of each tier | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| N random frozen shop units | where N >= 1 |
| N specific allies | where N >= 1, ally specified in effect condition |
| Self | applies to the unit that triggered it |
| Strongest ally | |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Swordfish

{{< figure src="https://i.imgur.com/u2wYc0d.png" >}}

* Trigger: start of battle
* Effect: deal damage
* Effect target: most healthy enemy, self

### Triceratops

{{< figure src="https://i.imgur.com/S5bSTAE.png" >}}

* Trigger: hurt
* Effect: stat change
* Effect target: 1 random ally

### Vulture

{{< figure src="https://i.imgur.com/RxnchxS.png" >}}

* Trigger: ally faints
* Effect: deal damage
* Effect target: 1 random enemy

{{< figure src="https://i.imgur.com/1vMK2z4.png" >}}

* Trigger: buy, sell
* Effect: stat change
* Effect target: 1 random ally

### Hyena

{{< figure src="https://i.imgur.com/BxMAzIx.png" >}}

1.
* Trigger: start of battle
* Effect: stat swap
* Effect target: all units

2.
* Trigger: start of battle
* Effect: shuffle
* Effect target: all units

3.
* Trigger: start of battle
* Effect: stat swap, shuffle
* Effect target: all units

### Lionfish

{{< figure src="https://i.imgur.com/KWwHh2a.png" >}}

* Trigger: before ally attack
* Effect: status effect
* Effect condition: limit triggers
* Effect target: enemy about to be attacked

| Trigger | Description |
| --- | --- |
| Ability damage | when the unit's ability deals damage |
| Ally ahead attacks | when an ally in front attacks |
| Ally ahead faints | when an ally in front faints |
| Ally ahead uses ability | when an ally in front uses its ability |
| Ally bought | when any ally is bought |
| Ally consumes item | when an ally is given an item |
| Ally faints | when an ally faints |
| Ally hurt | when any ally is hurt |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| Attack | when the unit attacks | 
| Any level-up | when any ally levels up |
| `Before ally attack` | `before an ally is about to attack` |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| Damage taken | when the unit takes damage |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy hurt | when an enemy is hurt |
| Enemy killed | when the enemy is killed as a result of this unit's attack |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Roll | when the shop is rerolled |
| Sell | when the unit is sold |
| Specific ally bought | when a specific ally or type of ally is bought |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Summoned | when this unit is summoned |
| Upgrade shop tier | when the shop levels up |

| Effect target | Description |
| --- | --- |
| All allies | |
| All allies ahead | |
| All classed allies | classed ally = of a specific class |
| All specific allies | specific ally = ally that passes a specific condition |
| All shop units | |
| All future shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| Any enemy hurt | |
| Any hurt | |
| Any levelled up | |
| Any that consumed item | |
| Attacking enemy | the enemy that just attacked this unit |
| `Enemy about to be attacked` | |
| Highest tier enemy | |
| Least healthy ally | |
| Most healthy ally | |
| Most healthy enemy | |
| Nth ally | where N >= 1 |
| Nth enemy | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N adjacent units | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N units in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random allies of each level | where N >= 1 |
| N random allies of each tier | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| N random frozen shop units | where N >= 1 |
| N specific allies | where N >= 1, ally specified in effect condition |
| Self | applies to the unit that triggered it |
| Strongest ally | |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

### Moose

{{< figure src="https://i.imgur.com/8R6Bp4e.png" >}}

* Trigger: end turn
* Effect: stat change
* Effect condition: mult lowest tier ally
* Effect target: 1 ally behind

| Effect condition | Description |
| --- | --- |
| If any specific ally | applies the effect if at least one ally passes a condition |
| If highest tier ally | applies the effect if this is the highest tier unit |
| If lost battle | applies the effect if the previous battle was lost |
| If player resource | applies the effect if a player's resource passes a condition |
| If specific ally | applies the effect if the ally passes a condition |
| Limit triggers | applies the effect up to a max # of times per turn |
| `Mult lowest tier ally` | `multiplies the effect with lowest ally tier` |
| Per turn number | applies the effect based on the number of turns |
| Per specific ally | applies the effect based on the number of allies of a specific type |
| Until the end of battle | the effect will persist until the next battle ends |

### Chili

{{< figure src="https://i.imgur.com/eHWT4Xm.png" >}}

* Trigger: attack
* Effect: deal damage behind

| Effect | Description |
| --- | --- |
| Add shop item | adds an additional item to the shop |
| Classify | adds a class to a unit |
| Copy ability | copies another unit's ability |
| Copy item to | copies this unit's item to another unit |
| Deal damage | deals damage to a unit |
| `Deal damage behind` | `deals damage to the unit behind the one that is attacked` |
| Double damage | chance to deal double damage to a unit |
| Discount unit | decreases a shop unit's cost |
| Discount item | decreases a shop item's cost |
| Faint | makes the unit faint |
| Gain item | gains a specific item |
| Give experience | gives experience to a unit |
| Give item | gives your item to a unit |
| Item effectiveness | add, sub, mul or div to item effectiveness |
| Kill | deals damage and kill a unit |
| Single stat swap | swaps stats within a unit |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Remove item | removes this unit's held item |
| Roll shop | rolls the shop |
| Set level | sets the unit's level to a specific value |
| Shuffle | changes the positions of multiple units |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Steal item | steals item from a unit |
| Summon | summons another unit |
| Take less damage | takes less damage from the next attack |
| Transform | transforms into another unit |

### Chocolate

{{< figure src="https://i.imgur.com/rNUWYD0.png" >}}

* Effect: give experience

### Sushi

{{< figure src="https://i.imgur.com/UU8Lvep.png" >}}

* Effect: stat change
* Effect target: 3 random allies

### Carrot

{{< figure src="https://i.imgur.com/ak927Uv.png" >}}

* Trigger: end turn
* Effect: stat change

### Pepper

{{< figure src="https://i.imgur.com/JmsnCOa.png" >}}

* Trigger: damage taken
* Effect: take less damage
* Effect: remove item

### Stew

{{< figure src="https://i.imgur.com/O3GUuay.png" >}}

* Effect: stat change
* Effect target: 3 random allies

### Taco

{{< figure src="https://i.imgur.com/EuwGp2Y.png" >}}

* Effect: stat change
* Effect target: 3 random allies

### Lemon

{{< figure src="https://i.imgur.com/laJWbaK.png" >}}

* Trigger: damage taken
* Effect: take less damage

## Final tables

[⬆️ Start](#start)  

OK, so now that this is all done we have a few tables that contain all the triggers, effects, effect conditions and effect targets that SAP uses.
This is what the tables look like:

| Trigger | Description |
| --- | --- |
| Ability damage | when the unit's ability deals damage |
| Ally ahead attacks | when an ally in front attacks |
| Ally ahead faints | when an ally in front faints |
| Ally ahead uses ability | when an ally in front uses its ability |
| Ally bought | when any ally is bought |
| Ally consumes item | when an ally is given an item |
| Ally faints | when an ally faints |
| Ally hurt | when any ally is hurt |
| Ally sold | when an ally is sold |
| Ally summoned | when an ally is summoned |
| Attack | when the unit attacks | 
| Any level-up | when any ally levels up |
| Before ally attack | before an ally is about to attack |
| Before attack | before the unit is about to attack |
| Buy | when the unit is bought |
| Consumes item | when the unit is given an item |
| Damage taken | when the unit takes damage |
| End turn | when the current turn (shop round) ends, but before battle |
| Enemy hurt | when an enemy is hurt |
| Enemy killed | when the enemy is killed as a result of this unit's attack |
| Enemy summoned | when an enemy is summoned |
| Enemy pushed | when an enemy is pushed |
| Faint | when the unit dies |
| Hurt | when the unit is hit |
| Item bought | when an item is bought |
| Level-up | when the unit levels up |
| Roll | when the shop is rerolled |
| Sell | when the unit is sold |
| Specific ally bought | when a specific ally or type of ally is bought |
| Start of battle | when the battle starts |
| Start of turn | when the turn (shop round) starts |
| Summoned | when this unit is summoned |
| Upgrade shop tier | when the shop levels up |

| Effect | Description |
| --- | --- |
| Add shop item | adds an additional item to the shop |
| Classify | adds a class to a unit |
| Copy ability | copies another unit's ability |
| Copy item to | copies this unit's item to another unit |
| Deal damage | deals damage to a unit |
| Deal damage behind | deals damage to the unit behind the one that is attacked |
| Double damage | chance to deal double damage to a unit |
| Discount unit | decreases a shop unit's cost |
| Discount item | decreases a shop item's cost |
| Faint | makes the unit faint |
| Gain item | gains a specific item |
| Give experience | gives experience to a unit |
| Give item | gives your item to a unit |
| Item effectiveness | add, sub, mul or div to item effectiveness |
| Kill | deals damage and kill a unit |
| Single stat swap | swaps stats within a unit |
| Multiple stat swap | swaps stats between multiple units |
| Player resource change | add, sub, mul or div of a player resource value |
| Push enemy | pushes an enemy to a different position |
| Repeat | repeats the effect its attached to |
| Replace item | replaces shop items with other items |
| Remove item | removes this unit's held item |
| Roll shop | rolls the shop |
| Set level | sets the unit's level to a specific value |
| Shuffle | changes the positions of multiple units |
| Stat change | add, sub, mul or div of a stat | 
| Stat copy | copies a stat from another unit |
| Stat give | gives a stat to another unit |
| Stat set | sets a stat to a specific value |
| Status effect | applies a status effect to a unit |
| Steal item | steals item from a unit |
| Summon | summons another unit |
| Take less damage | takes less damage from the next attack |
| Transform | transforms into another unit |

| Effect condition | Description |
| --- | --- |
| If any specific ally | applies the effect if at least one ally passes a condition |
| If highest tier ally | applies the effect if this is the highest tier unit |
| If lost battle | applies the effect if the previous battle was lost |
| If player resource | applies the effect if a player's resource passes a condition |
| If specific ally | applies the effect if the ally passes a condition |
| Limit triggers | applies the effect up to a max # of times per turn |
| Mult lowest tier ally | multiplies the effect with lowest ally tier |
| Per turn number | applies the effect based on the number of turns |
| Per specific ally | applies the effect based on the number of allies of a specific type |
| Until the end of battle | the effect will persist until the next battle ends |

| Effect target | Description |
| --- | --- |
| All allies | |
| All allies ahead | |
| All classed allies | classed ally = of a specific class |
| All specific allies | specific ally = ally that passes a specific condition |
| All shop units | |
| All future shop units | |
| All summoned allies | |
| All pushed enemies | |
| All summoned enemies | |
| All unfrozen shop units | | 
| All units | |
| Any bought | |
| Any enemy hurt | |
| Any hurt | |
| Any levelled up | |
| Any that consumed item | |
| Attacking enemy | the enemy that just attacked this unit |
| Enemy about to be attacked | |
| Highest tier enemy | |
| Least healthy ally | |
| Most healthy ally | |
| Most healthy enemy | |
| Nth ally | where N >= 1 |
| Nth enemy | where N >= 1 |
| Nth shop unit | where N >= 1 |
| N adjacent units | where N >= 1 |
| N allies behind | where N >= 1 |
| N allies in front | where N >= 1 |
| N units in front | where N >= 1 |
| N random allies | where N >= 1 |
| N random allies of each level | where N >= 1 |
| N random allies of each tier | where N >= 1 |
| N random classed allies | where N >= 1, classed ally = of a specific class |
| N random enemies | where N >= 1 |
| N random frozen shop units | where N >= 1 |
| N specific allies | where N >= 1, ally specified in effect condition |
| Self | applies to the unit that triggered it |
| Strongest ally | |
| Two adjacent units | applies to 2 units adjacent to the one that triggered it |
| Two adjacent allies | applies to 2 allies adjacent to the one that triggered it |

We could do some refactoring here. Removing some things that are repetitive, adding some that are missing that are obvious, and so on.
For instance, there are effect targets for "least healthy ally", "most healthy ally" and "most healthy enemy". There's obviously one missing,
which is "least healthy enemy". 

Similarly, we can see that often there are effect targets for allies, enemies and shop units. So we could add "most healthy shop unit", "least healthy shop unit" as well.
We can also see that there's a distinction between frozen and unfrozen shop units, so we could add "most healthy frozen/unfrozen shop unit", "least healthy frozen/unfrozen shop unit".
There's also "strongest ally", which is a different calculation than "most healthy". And it's also missing "strongest enemy", "strongest shop unit", etc.

You get my point, right? We can go from the things that SAP uses to a lot more that come obviously from just looking at the list. One of the benefits of doing an exercise like this
is that if you choose the right level of abstraction, just looking at the tables generated gives you a lot of ideas for new gameplay.

Another benefit is that you can now just combine things from the different tables to create new units. There's a total of 33 triggers, 34 effects, 10 effect conditions and 40 effect targets.
So I'm just going to go on [random.org](https://www.random.org/) and generate 3 random numbers from 1-33, 1-34 and 1-40. I'm going to omit effect conditions from this because they're too specific, so it's
best to add them manually depending on what comes out.

The numbers: 13, 5, 11. This corresponds to:

* Trigger: before ally attack
* Effect: deal damage
* Effect target: all units

Well this sounds disgusting. But I can imagine it working if you keep the damage real low and add some limits. Something like:

#### Locust - 1/1 - Tier 3

Lv.1: Before friend attack -> Deal 1 damage to all pets. Works 2 times per turn.  
Lv.2: Before friend attack -> Deal 1 damage to all pets. Works 4 times per turn.  
Lv.3: Before friend attack -> Deal 1 damage to all pets. Works 6 times per turn.  

It's a locust because of locust swarms that deal lots of small damage! Maybe it would be cool? Let's try another. The numbers were: 19, 24, 9. This corresponds to:

* Trigger: enemy hurt
* Effect: set level
* Effect target: all summoned enemies

This sounds positively weird and way too specific, but maybe something like:

#### Panther - 5/5 - Tier 2

Lv.1: Enemy hurt -> Decreases the level of summoned enemies by 1.  
Lv.2: Enemy hurt -> Decreases the level of summoned enemies by 2.  
Lv.3: Enemy hurt -> Decreases the level of summoned enemies by 3.  

Doesn't seem very cool or useful to me... I chose panther because it's kind of the opposite of white tiger... Let's try a last one. Numbers: 23, 14, 15. This is:

* Trigger: faint
* Effect: item effectiveness
* Effect target: any hurt

This one initially doesn't seem to make much sense but I think it's cool. The first thing to notice is that for any other unit that uses "item effectiveness" it doesn't really have a target.
So we can safely ignore the effect target for this one, which is good because it doesn't make much sense anyway.

So we're left with something that increases item effectiveness when it dies. Which means we could go for a canned food type of deal but instead of increasing the stats of shop units, it increases
the stats of shop foods. The only thing left to consider is that this would have to happen only outside of combat, but there are other units with the "outside of combat" modifier. So we could go for something like:

#### Can't think of an animal - 3/2 - Tier 2

Lv.1: Faint outside of combat -> Give all current shop foods +2 to attack and health effects.  
Lv.2: Faint outside of combat -> Give all current shop foods +4 to attack and health effects.  
Lv.3: Faint outside of combat -> Give all current shop foods +8 to attack and health effects.  

So whenever you make this unit faint outside of combat (via pill, praying mantis, etc) it gives any current food shop a bonus to its attack and/or health effects.
If there's a pear on the shop and you sell this unit at Lv.2, then the pear will give a total of 6 attack and health instead of the original 2.

Of course you could change this to give it to all current and future shop foods, like the canned food, but then you'd have to find mess around with it more to balance it properly.

## Rerolling shop genre

All of this shows that Super Auto Pets is both very cleverly designed and also very expandable. It has a clear set of composable parts that work well together, but most importantly, that work well on *any
rerolling shop game*. Rerolling shop games generally have the following features:

* There's a shop that offers units and can be rerolled
* The shop has levels and can be levelled up
* Units can be bought, sold, locked
* Units have levels and can be combined to level up
* Units have positions in relation to one another
* Units can hold items
* There's a distinction between shop phase and combat phase

Maybe there are a few I'm forgetting, but the more of these features a game has, the more it can use SAP's mechanics. For instance, in SNKRX the ability to freeze individual units doesn't exist, which means that I can't
make any effects that make use of the frozen/unfrozen distinction.

In both SNKRX and Brotato, the units (which are the guns in Brotato) can't hold items, which means that we can't use any effects that have to do with items. 
In Just King, on the other hand, units can hold items, which means that things like "copy item", "give item", "item bought", etc, can be used by it. 

In pretty much all rerolling shop games units have positions relative to each other, which means that all effects having to do with "ahead", "behind", "nth position", "adjacent" and so on can be used by them.

The point being that because SAP covers so much ground for all common ideas that exist in rerolling shop games, it can safely be used as solid ground to build from.
Of course, a lot of its ideas exist in other games too. Lots of card games by definition will have notions of triggers and effects, and its not uncommon to see, for instance, a "trigger: hurt" out in the wild.

But what makes SAP unique to me is that it combines ideas specific to rerolling shop games and builds upon them in a very thorough and creative way.
So if you're making a rerolling shop game you should 1000% play SAP and get used to its mechanics, because using them will very easily make your game better.
