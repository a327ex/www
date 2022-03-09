+++
title = "Super People design review"
tags = [
    "design",
]
date = "2022-03-09"
images = ["https://i.imgur.com/AKSEJnM.png"]
+++

I've played [Super People's closed beta](https://store.steampowered.com/app/1190340/SUPER_PEOPLE/) for about 300 hours for the past month or so. I have a pretty good understanding of the game by now and I managed to reach a good rank 
(~#40 global, although if the game was properly populated I'd barely be able to reach top 500 at most, since I'm not *that* good). The point being that everything I'll say comes from a place of good and fair experience.

{{< figure src="https://i.imgur.com/5Aj6pfB.png" >}}

The main reason for writing this post is that Super People has a few interesting design problems that tie in with issues I've been thinking about recently relating to [openness](https://en.wikipedia.org/wiki/Openness_to_experience), [conscientiousness](https://en.wikipedia.org/wiki/Conscientiousness) and game design so I thought it'd be worth writing it down.

## Overview

Super People is a battle royale that's most easily described as *very similar* to PUBG. It has all the same mechanics, the same setup, many of the same weapons and attachments, the same UI (which I assume comes from an asset pack),
and so on. On top of that EVERYTHING is executed better. Animations, shooting, vaulting/parkouring, driving, networking, map design, and so on are *all* significantly better.

The one that really impressed me was that the game feels fine to me even when I'm playing with 200+ms. Since there weren't many SA players and I'm from Brazil, I'd usually get matched to US-east servers (120ms) or US-west ones (220ms).
And while there is some noticeable delay in some actions on US-west, I rarely felt cheated or that something happened or didn't happen due to lag.

Surprisingly, I also never felt that way about other players, because it could easily be the case that the game favors the person with higher ping. But occasionally you'd get a korean matched on US servers and fighting against them
never felt unfair, so whatever the devs are doing with their netcode is really good.

In any case, the main difference SP has to PUBG is that SP has some heavier RPG elements, namely classes (with ults), passives, and gear upgrading.
Most of the problems the game has happen here, and I'll go over them in some detail as well as how I'd change them to make the game better. But before that, some overview of the game's

### Classes

SP has 12 classes that offer some pretty varied playstyles. To give you an idea of what classes enable, let's start with the teleporter.

The teleporter class is my favorite and like most classes in the game it has an ult that's extremely versatile, as it lets you teleport to any nearby location with a two minute cooldown.
All you do is press G, click somewhere on the map that's in range, and then you're instantly there.

This is a very well designed skill because it's simple, effective, and can be used offensively, defensively or for utility. For instance, here's an example of an offensive use:

{{< youtubestartend jvVDBGZsd5M 5040 >}}

You hit someone, they hide behind something and then you teleport on top of them and kill them. Or this:

{{< youtubestartend jvVDBGZsd5M 2180 >}}

You hit someone, they hide behind a rock to heal, and then you teleport behind them. In this case this was a fairly messy teleport, usually you want to do it precisely and turn towards where the enemy will be before
teleporting, since experienced players will hear you teleport behind them and you won't get that much time to finish them off.

You can also use it defensively, like so:

{{< youtubestartend jvVDBGZsd5M 2575 >}}

Here a nuclear player uses his ult, which, well, nukes a fairly big area and can kill you instantly if you don't escape, so the teleport is used defensively to avoid that. But generally defensive uses will involve an engagement
with poor positioning where you have low chances of succeeding, like say you got caught off guard and some guy almost killed you, now you're hiding behind a tree and the circle is coming behind you while the guy in front of you
just waits since he knows you have to move soon. In this case a teleport saves you perfectly.

Finally, for utility, you can use it mostly to get in and out of high ground easily, especially in positions that are impossible for non-teleporters to get to, which always surprises people, like so:

{{< youtubestartend jvVDBGZsd5M 5385 >}}

Another class that has a versatile kit is the strike force. His ult lets you run really fast and jump really high for a short duration, and like the teleport, can be used offensively, defensively or for utility.
As an example of a failed offensive use:

{{< youtubestartend 6UB2H3Jmq2U 3950 >}}

Ideally you want to avoid running in a straight line when approaching, but you also want to kill the enemy while in the air, since after you land there's usually a very slow recovery animation that leaves you vulnerable.
There's also utility uses, here for getting from one place to another quickly and getting on top of a building:

{{< youtubestartend 6UB2H3Jmq2U 1475 >}}

As for defensive uses there are these two examples against shotgun masters:

{{< youtubestartend RzgiT8naKmI 1010 >}}

In this first one the shotgun master is trying to get close because he has an SMG and a shotgun, both weapons which deal more damage the closer you are to your enemy. He uses 2 flashbangs to achieve this, missing the first
and connecting the second, and also using his ult, which is a super jump that can be used as a gap closer, since people will have a hard time shooting you while you're in the air and they'll also have a hard time figuring out
where you landed.

In this case strike force's ult is used defensively to give some distance from the shotgun master. The same happens in this fight against another shotgun master:

{{< youtubestartend RzgiT8naKmI 1170 >}}

These shotgun masters weren't very good, but if you play against good ones they really don't give you that much of a chance to run away. Interestingly, that's currently the most OP class and the most favored one amongst very good
players, but simultaneously the most hated one among normal players.

I also don't really like it since it takes quite a lot of skill and good decision making to consistently get close to enemies without getting punished, which the best players manage to do constantly because the super jump
ability can be used offensively as a gap closer but also defensively, so what they do is that as soon as their HP drops too much (shotgun master has the highest HP pool of all classes) they just jump up, either to hide somewhere
or to heal and give themselves a few seconds.

The only way I personally can somewhat consistently beat good shotgun masters is with the gas soldier class, which has a close range ult that deals almost your entire HP in damage:

{{< youtubestartend jvVDBGZsd5M 3660 >}}

In this case you just hear someone shooting nearby and shoot the ult, and since it can go through walls it will deal a lot of damage to everyone it touches. With the good shotgun masters though what I end up doing is trying to
sneak up on them, waiting for them to use their jump as they fight someone, and then use my ult as they won't be able to escape it. Even in that case sometimes I still fail because good players are just 100% aware at all times,
but sometimes it works.

Anyway, the point being, the game has a lot of classes, they're all very varied and they're also fairly well designed. But on top of ults all classes also have 9 passives and a weapon specialty selected at random,
here's a screen showing it all:

{{< figure src="https://i.imgur.com/IQbXBOC.png" >}}

The 9 passives are also fairly varied, and they can be actual passives but sometimes they're also actives. They similarly can also be offensive, defensive or for utility. Some simple examples:

{{< figure src="https://i.imgur.com/Fml6h36.png" >}}

{{< figure src="https://i.imgur.com/UiCyEi6.png" >}}

{{< figure src="https://i.imgur.com/MdGivDF.png" >}}

{{< figure src="https://i.imgur.com/6fDOiZm.png" >}}

{{< figure src="https://i.imgur.com/OZDwdgb.png" >}}

These are simple passives that give you more damage or defense based on different conditions that make sense for your character. So for instance, the third one gives you more damage for sniping, which makes sense
as it's a passive for the sniper class, while the last one you gives you long range damage resistance because strike force wants to be close to enemies, so it can be used to make it easier for you to close the gap between an enemy.

Lots of passives give you utility though, like these:

{{< figure src="https://i.imgur.com/FoImPR3.png" >}}

{{< figure src="https://i.imgur.com/iK6y6jr.png" >}}

Both of these are from the seeker class, and the first one basically tells you whenever there are enemies nearby. You can't exactly tell where they are because it flashes a somewhat big circle, but you get a very good general idea.
And the second passive is a literal wall hack. You press 4 and now you have a sensor and if you keep holding it down you can see where people are through walls. Very OP but it has a fairly small range. Example of it in use here:

{{< youtubestartend gdqtTf9vADg 4720 >}}

For an active instead of passive, the nuclear gets an RPG to her 4th slot. You can see how it works here:

{{< youtubestartend jvVDBGZsd5M 8965 >}}

Some of the passives also can change how grenades work:

{{< figure src="https://i.imgur.com/WD2Kqzc.png" >}}

{{< figure src="https://i.imgur.com/6ICJ1VH.png" >}}

{{< figure src="https://i.imgur.com/8BQeW9w.png" >}}

{{< figure src="https://i.imgur.com/e3h1B4E.png" >}}

{{< figure src="https://i.imgur.com/rmndvq7.png" >}}

And there's even one that gives you C4, which is like a grenade but it sticks to walls and can deal damage through them:

{{< figure src="https://i.imgur.com/yuBE1dh.png" >}}

And there's also one passive from the gas soldier that gives you a damage + HP buff whenever you drink fuel:

{{< youtubestartend jvVDBGZsd5M 3585 >}}

The game pretty much took every element that exists in PUBG and other battle royales and added some variety to each element via the passive system. Every system, driving, grenades, vaulting/parkouring, leaning, sniping, using fuel,
parachuting, and so on, for every element there's a passive in some class that augments or changes that element in some way.

This, coupled with all the ults for each class, adds A LOT of variety to the game. Not only do you have to learn how to play each class and make best use of the passives you have, but you also have to learn how to play against
each class and this creates a really long but fun learning curve.

Another thing is that at the start of each round you're given a class at random. You can reroll your class once by spending 100 gold, or choose a specific class for 500 gold. You can spend 100 gold every round just fine
without running out of it, but you can't spend the 500 without running out eventually, unless you really focus on getting gold in each round which is kind of annoying. This essentially forces people to try out different classes which
adds even more variety to everything.

The fact that the game has so much inherent variety to it is an important point to understand that I'll focus on more later, but I went through the trouble of describing many of the ways in which this happens so that anyone who
hasn't played the game can have an idea of how thoroughly the devs changed the game when compared to PUBG or even the more wacky random BRs like Fortnite.

### Levelling

The other element that the game has, and this one is much simpler to understand, is levelling up. Every player has a level that goes up to 27, and on each level up you gain one ability level for one of your 9 passive abilities.
Each ability goes up to level 3 at most, and at player level 10 you also gain your ultimate. You also gain 2 levels every time the circle shrinks, and you can level up your abilities faster by finding capsules of different colors
around the map. For instance, if you find a red capsule and use it then you'll gain one level for one of your red abilities.

You also have five pieces of gear: two weapons, a helmet, an armor and a backpack. All of these have five levels that can be increased through upgrades which happen by finding materials throughout the map, and the game automatically
marks nearby materials that you need for your specific items. If you watch early gameplay of a round, most of it consists of running around, finding gear and materials and upgrading your items:

{{< youtubestartend jvVDBGZsd5M 210 >}}

This is quite different from PUBG, which has no crafting at all (or had none when I played it). Most western BRs have some crafting, but from what I've seen they generally take the form of a forge/replicator/crafting bench somewhere
on the map, rather than the sort of open crafting that SP has. A few korean BRs seem to have this similar style of crafting as to SP, [Eternal Return](https://store.steampowered.com/app/1049590/Eternal_Return/) being the most popular
that I know of.

Regardless, the effect this has on the game is that it makes each playthrough feel somewhat grindy. You don't want to fight people undergeared, since if they're properly geared and you aren't they have a higher chance of winning
fights, which forces you to spend the early game making sure that your gear is appropriate, which makes the game kind of grindy and more boring than it should be.

## Openness & conscientiousness

Now that you have some idea of how the game works I can get to the main point of this post, which is a personality based analysis of Super People's design. There are two main components that are relevant here which are openness
and conscientiousness.

Openness refers to someone's interest in exploration, variety, borderlessness and generally new things. The image below is an example of a highly open mechanic:

{{< figure src="https://i.imgur.com/mexPXlo.png" >}}

A skill tree like this is just pure exploration and variety and thus it's something that appeals massively to the highly open. Another similar example:

{{< figure src="https://i.imgur.com/nAmcSt5.png" >}}

Any game with hundreds of items like this and where on each playthrough/run/round you are given a random set of them is also going to appeal to the highly open, as you're constantly being showered with new things that combine
in different ways.

As for conscientiousness, it's about process orientation, predictability, organization, discipline, borders and generally order. The image below is an example of a highly conscientious set of mechanics:

{{< figure src="https://i.imgur.com/rb7BDDD.png" >}}

Conscientiousness subdivides into orderliness and industriousness, and so generally all games that are simulating industry are going to appeal to those traits a lot. As an example of a very low openness but medium/high
conscientiousness type game we can look at this:

{{< figure src="https://i.imgur.com/J4SYAbJ.png" >}}

This is your average MMO. You have your NPCs, quests, quest markers, some games have autopathing to where you have to go do your quests... It's very on rails and exploration-free, but also very relaxing for someone who just wants
to sit down and spend some time doing something fairly mindless. And it also tends to be fairly grindy, which appeals to the industrious nature of the highly conscientious.

You can even look at my game for instance:

{{< figure src="https://i.imgur.com/GqOZVvA.png" >}}

The auto chess formula where you have to combine different units to gain bonuses and also take care of your economy has a good mix of both traits in it. Finding out about new classes, new builds and combos, etc, appeals to the
highly open, whereas building an economy, figuring out when to spend vs. when to save appeals to the highly conscientious.

In general any time you have accumulation of resources you're appealing to the more conscientious because that's something they really enjoy. This is one of the reasons why they like grinding in MMOs, or gacha games,
or ARPGs and so on.

This is also very visible with roguelites, for which there's a big divide from a high level design perspective of "pure" roguelites vs. roguelites with cumulative progress between runs. The pure ones appeal more to the highly
open, whereas the ones with cumulative progress appeal more to the highly conscientious. This also explains why most gamedevs prefer the pure ones, as gamedevs tend to be higher in openness (since that's what's needed
to be a creative person).

The solution that most devs settled on that felt less wrong was to keep each run relatively pure, but to have unlocks between runs that get added to some pool of items. This appeals to the conscientious nature in people since they
are "building" something in between runs, but without actually letting power leak into each run, thus keeping them pure. This is an example of a good solution that is harmonious for all personality types, even though the games with
actual progress between runs (like say Hades) will appeal more strongly to the highly conscientious.

And this is also without taking into account that a roguelite by itself is a highly open type of game since it's all about exploration and variety and so on. For a roguelite that goes very hard on appeal to the highly open
we can look at Noita:

{{< figure src="https://i.imgur.com/rVMXeux.jpeg" >}}

I've played Noita very briefly so correct me if I'm wrong. But as far as I understand it in Noita there's no progression nor unlocks between runs. It's the purest type of roguelite you can get. But it also happens that there's quite
a lot of exploration you can do in any given run, to the point where most Noita threads I see are all about discussing lore and the mysteries the game has rather than the gameplay.

This is something that also appeals to the highly open because openness subdivides into two rough categories: openness and intellect. Intellect largely maps to what I've talking about so far, the need for exploration, variety,
combining existing things into new ones, and so on. Whereas openness maps more to affinity towards aesthetics, art, and the more softer and spiritual types of things you would attach to "openness to experience". In games, this softer
type of openness maps more to an interest in lore, mysteries, story, fantasy, etc. So Noita is a game that fully appeals really well to both subtypes of openness, while not appealing at all to the highly conscientious.

This is one of the reasons why I think despite being a great game, it has about 40k reviews, compared to the 120k+ that most of the other great roguelites of similar quality have. Because the game is designed to appeal
only to one personality type its potential audience is lower, and thus despite being a really popular game and having the potential to be one of the really big ones, it fails to get there. This isn't to say that this is a bad thing,
of course, but just to highlight how important it might be to look at high level design decisions from a personality perspective, since they can help you place your game more correctly with respect to the kinds of audiences you
want playing it.

For another game that has a good combination of appeal to the open and the conscientious we can look at the recently released Elden Ring. Especially, this video which somehow made its way to my feeds:

{{< youtube 4HF9lYsLQN4 >}}

Here Asmongold is essentially complaining that he isn't highly open enough to deal with the game's exploration requirements, which makes sense, since he's an MMO player. AFAIK he's still playing the game but this is a very good
example of how these traits manifest in individuals. Notice that he has a hard time explaining exactly why he doesn't like that aspect of the game, since people generally don't have the concept of "openness" in their heads.

And of course, this discussion surrounding Elden Ring's general lack of direction also creates images such as:

{{< figure src="https://i.imgur.com/uPIvv2t.png" >}}

People inherently understand that this is wrong, despite plenty of games being EXACTLY like this, because they can intuitively sense that Elden Ring is properly designed and doesn't really need any of the UI markers.
However it's also important to understand that the people who are asking for more direction in a game like Elden Ring aren't necessarily wrong, they just have a different personality. It's fine if the game doesn't cater
to their particular personality type, but it's important as a developer to understand that they aren't *objectively wrong*.

In any case, you can even see this division even when people look at what went wrong with matchmaking systems over the past decade+:

{{< figure src="https://i.imgur.com/6jU01CR.png" >}}

Here the "wacky gamer" is someone more open, they like exploration, variety and borderlessness. Whereas the "stoner zone" is someone fairly low in openness (not necessarily high in conscientiousness) who just wants to do the same
thing over and over and relax. This would be the equivalent to Asmongold and MMO players in general. Finally the "hardcore gamer" is someone low in agreeableness and high in conscientiousness, and that mix tends to end up
being highly competitive.

All of these examples to say that this divide exists in people and it's clearly visible via different game mechanics and who they end up appealing to. But the most important thing of all is that if you're designing a game you
want to create your mechanics such that they appeal to all personality types in a harmonious way.

The big five personality index is a good tool for AoE behavioral analysis, that is, understanding how groups of people behave. But it's also a very high level and low resolution tool. You could think of the biological behavior of 
groups of people as the highest level of analysis possible, and then the assembly code that runs on the computer as the lowest level possible.

To make a good game, you want all levels of analysis, from the highest to lowest, to be harmonious. Any feature you add into the game should make sense from a personality perspective, from a general game design perspective (is it fun),
from an actual implementation perspective (does it feel good to play), it should work well with other mechanics, and it should also run properly at 60fps and without bugs.

People can intuitively tell when a game comes together at all those levels, and they can also intuitively tell when it doesn't. And so you want your games to come together in this way... Which brings me to

## Super People's design

As I just mentioned, you want all aspects in your game to align, and the highest level of analysis you can start with, that also happens to be the lowest effort to change generally, is with personality traits.

In a battle royale we can see that the base game itself is competitive in nature, and so by default it's something that's going to appeal to the a lot to the highly disagreeable and somewhat to the highly conscientious.
But because the game emulates such a fundamental set of actions, which is what both animals and humans have evolved to do - you know, hunting, being hunted, finding food/resources, and all that wrapped up in a higher order
goal/plan (not dying to the circle and winning) - we can say that this is a very neutral and pure type of game from a personality perspective, meaning, it's going to make use of all your traits equally and none of them are
going to be too favored over another, which helps explain the popularity of the genre, since it just naturally appeals to everyone.

Knowing this, we can start looking at other elements in SP individually:

### Classes and class selection

By definition the addition of classes adds variety to the game, which favors the highly open. Even if all you do is play with a single class, you still need to learn how to play against the other 11 and learn the intricacies
of each match up.

The way class selection currently works in SP doubles down on this, since you can't reliably choose one class to play at all times. This IMO is an even bigger push towards openness than the addition of classes, since here you
start messing with how people learn. There's this meme about breadth-first vs. depth-first learning:

{{< figure src="https://i.imgur.com/frQjOMf.png" >}}

Which is nothing more than the distinction between openness and conscientiousness. The highly open will be mostly breadth-first learners, since they like variety and exploration more, whereas the highly conscientious will be
mostly depth-first learners because they are more process oriented and bordered and so on. This of course doesn't apply only to learning, but to thinking, doing, etc.

For instance, I'm very obviously highly open, and you can tell from the way I write my articles alone. Despite this article being laid out linearly, it's clearly a very circular type of post. I'm pulling out lots of examples
and circling around a point, and then once enough examples have been given I can very easily make the point, as once you've seen enough instances of it it's obvious what binds everything together. And then this point gets repeated
further because now it's a part of a knowledge structure and so you can start using it as a symbol more easily and so on.

This way of thinking is very common and it's also very common for people who aren't highly open to generally reject it. There are many people who can't follow arguments of this type and when they encounter someone doing it
they will say things like "why is that guy so rambly, why does he take so long to make his point".

When it comes to games this also matters, as if people are forced to play random classes instead of classes they want to play then as a designer you're favoring the highly open
at the cost of everyone else. In genres like roguelites this may be desirable, since roguelites are by default an open genre, but for something like a BR which is neutral (and which also needs tons of players to work)
you're probably better served not forcing your hand too much either way.

People want to be able to play a single class, learn how to play against other classes, get really good at it, and only then start venturing out into playing other classes. It's just how a good portion of the population
approaches things and there's nothing that can be done to change this.

So the solution for SP here is simple: let people choose their class freely. If as a designer you want to encourage variety then also add a button that lets people
play a random class and give out a gold reward for anyone who chooses this option, for instance.

The game already adds classes, which adds lots of variety to an otherwise pure genre, so you don't want to double down on it and force even more variety on people without really good reasons.

### Levelling + passives

The addition of a levelling system to SP becomes necessary from the addition of classes. This is due to the simple fact that different classes have different strengths and weaknesses, and as a designer you want to be able
to balance around those differences by changing a few numbers around, things like HP, movement speed, attack, defense, and so on. One of the easy ways to achieve this is to have a levelling system, and to have different
ratios for different stats for each class.

This is something SP already has, like, for instance, generally melee oriented classes have a higher HP pool and/or defense. But this levelling system also plays well with the passive system, since it also lets you give out
one passive per level randomly, which adds some variety to how each game goes since you can't rely on having specific passives early on.

As an aside, one thing that some people really don't like about SP is that it has a higher TTK (time to kill) than most BRs, certainly higher than PUBG. But this, again, is a necessary change due to the addition of classes.
If everyone has passives and ults and whatnot, it would feel really bad if you got instantly killed without having even a chance to defend yourself using your abilities, so the higher TTK fixes this problem.

Overall I wouldn't change anything about the levelling and passive systems, as they feel like inoffensive and necessary changes to the BR formula and they're also integrated into the game well enough to be harmonious.

### Gear grinding

This system goes back to the Elden Ring meme full of markers. Having nearby materials shown to you at all times acts like the markers do in an open world game, it turns the game into this MMO-like grind that takes
away from the purity of the BR formula.

While I personally disagree heavily with SP's gear grinding system, it's important to be able to see the other side's argument clearly. And the argument for markers generally is that people who are low in openness
don't like exploring and they also don't like not really knowing what to do.

Like the "stoner zone", they just want to sit down and play a game and relax for a few hours after a hard day of work. In my MMO days plenty of people in my guild were literally like this. They'd come home from work
and play for their 4-5 hours a day. Every day, at the exact same time. They'd generally be behind the rest of the guild since most people would play for longer periods, but they were extremely consistent and eventually caught up.

This is a perfectly valid type of person to cater to in your designs. In fact, SNKRX itself caters to this personality really well. And so does Vampire Survivors. In both games you just sit down and you get a lot out of pressing
a small amount of keys and paying very little attention to what's happening. They're perfect games to zone out to...

[**HOWEVER**](https://www.youtube.com/watch?v=351Aa5q_S98)

Battle royales are not really the kinds of games that you want to relax to, right? It's a very competitive genre by nature and you're thrown into an environment where you just need to pay lots of attention if you want to do well.
You're being hunted, after all. So catering to people who just want to zone out pretty much goes against the core of genre.

The other main argument you could make is that when people are thrown into an environment and not given any directions they'll feel lost, and so the game automatically telling them where to go via nearby materials being shown
is a small way to direct the directionless, which I think is an argument that has some weight.

When I played PUBG the biggest lesson I learned was that I needed to plan more. Essentially, I'd play the game by roaming around aimlessly and it turns out that that puts you in a sort of prey state that increases your stress levels.
If you have no goal/plan and you're just wandering around aimlessly you're going to do worse in these games not only because you're more jumpy/fearful/stressed, but also because if something goes wrong there's less you can learn from
it, since you had no plan to look back on and go "which part of the plan went wrong".

So the argument that could be made here is that adding material markers gives people some small amount of direction so that they aren't wandering as aimlessly. But this feels like a weak argument because now that they were given
this tool that allows them to not think, they'll be even more aimless and will just follow the material markers without any planning. So in the end it also doesn't help.

Overall my solution for this system is to remove it completely. Gear should be found across the world randomly at various levels. So you find Lv.1 armor or Lv.4 armor randomly like you can now, and you can't really know for sure
that if you just grind out the materials you'll be able to have a full Lv.5 set of gear.

This feels harmonious and makes sense. If you have a match that lasts 30 minutes (if you get to the end) it feels like a mistake to add like 10 minutes of grind to it before you can actually fight other people fairly.
And if you look at other games that have rounds of this duration (like say roguelites) they also don't make this choice of adding a very grindy step to the main gameplay, all the grind happens between runs, in what I call
the "meta gameplay", which are all the systems around the game that aren't the actual game, like unlocks, achievements, etc.

There are a few unintended consequences of removing material grind out of SP, like, for instance, making the driver class more OP. The driver is a class that can summon a very good vehicle as an ult at level 10, but it can also
summon a normal vehicle at level 1. So, if you look at a map of the game:

{{< figure src="https://superpeoplewiki.com/assets/img/maps/orbisland.jpeg" >}}

One thing you notice is that like most BRs, there are "urban" and "rural" areas. Urban areas have higher loot density, whereas rural ones have lower. The driver class enables a player to drop in rural areas only and move between
them quickly, since it has a car from level 1, which means that it can loot at the same speed (or faster) than someone in an urban area, with way lower risk, since most people drop in urban areas rather than rural ones.
So removing material grind from the game makes the driver more OP because he simply can cover more ground and find more impactful loot (rather than materials) without having to worry about fighting other players as much.

There are many possible ways to fix this, like increasing loot quality in urban areas, but this unintentionally buffs classes that benefit from being in urban areas, like the SWAT. You can also just directly nerf the driver,
but I personally would just make a change like this and then wait and see. Currently the most problematic class in the game is the shotgun master, so it probably makes sense to do things to buff other classes instead and see
how people react to the changes.

So overall, remove all gear grind and materials, and let people find items purely randomly.

### Personal supply

Super People also has a personal supply system. The personal supply is a box that you can open in game for gold (which you also get in game, but that persists between rounds, so you can build up a gold amount
in your account) to get specific items that you defined before a round started. By default you get a heroic version (Lv.5) of your specialized weapon, as well as some ammo and a medkit. But you can also add up to 5 items
and then when you open the box in-game those items will be there:

{{< figure src="https://i.imgur.com/FYfHQmz.png" >}}

{{< figure src="https://i.imgur.com/BoNFfFR.png" >}}

This makes sense if you want to add some predictability to any given round, like, for instance, if you're playing the marine class, it gets a 20% damage buff when your weapons are using silencers. But silencers are somewhat
rare to find because they're arguably the best attachment in the game, so to get around the fact that you're probably not going to find them you can add them to your personal supply. Similarly, if your specialized weapon is the X40A1
sniper rifle, it's way better to use it with an extended magazine, except that the one it needs is one specific for snipers which is also hard to find, so it makes sense to add it to the personal supply.

Another example are shotgun masters, who absolutely need their super jump, which is a blue passive/ability rather than their ult. Being a blue passive/ability it can happen that by the time the personal supply drops you still don't
have it since passives are given out randomly, and since you absolutely need it to play the class properly, as it's functionally your ult, it makes sense to add multiple blue capsules to the personal supply.

Essentially this system is a way of adding some consistency and predictability to the game. The more items you add the more gold it costs to open the box, so currently it's not something you can do every single round,
but it still works well enough for the purpose its supposed to serve. This is a system that I wouldn't really change.

### Armory

Finally, the armory system. With this you can craft specific weapons that deal less damage than normal but have special effects. You can craft these weapons with blueprints that can be found in-game, either as random loot or when
they drop from when a player dies. This is IMO the weirdest system that the game has. It's definitely a grind and also adds some predictability to your matches, so it definitely appeals to the conscientious side, but the fact that
the special effects crafted weapons get are chosen randomly makes it somewhat unharmonious.

{{< figure src="https://i.imgur.com/BjCAZpy.jpeg" >}}

If you look at the image above you can see a mythical M416S, which is the highest level (7) a weapon can reach, with the maximum number of special effects added to it. As you can see from the effects they're not really very interesting
or impactful at all. That, coupled with the fact that they're random, makes this system really kind of lame.

I would change this so that weapon effects are both way more impactful and also not random. So if you craft a mythical weapon you can choose maybe 3 effects, and they'll be things like +25% headshot damage or something, and not -4%
enemy accuracy if you shoot the enemy's legs. This makes the game more unfair, in that a player with a Lv.500 account who has crafted the best weapons will always do better than a player with a Lv.1 account who's on their first match,
but it's the kind of price you have to pay to appeal to people who enjoy building out their accounts over time.

## Summary

So to summarize, here's what the game's system currently look like:

* Classes: adds variety to the game (+open)
* Class selection: random class selection adds even more variety (+open)
* Levelling + passives: predictability and grinding, but passives are random (neutral)
* Gear grinding: adds quite a lot of grinding to each round (+cons)
* Personal supply: adds some predictability to each round (+cons)
* Armory: adds some predictability and grind, but weapon effects are random (neutral)

And so if we look at this we have a game that's roughly neutral on the whole, with some additions favoring the highly open, some favoring the highly conscientious, and some pulling both ways and ending up neutral.
Given that the base game itself is somewhat neutral, except that it doesn't appeal to those low in openness, but we have a system that fixes that (gear grind + material markers), we could look at this and say that
the game is very well balanced personality wise.

But as I mentioned before, all these elements have to align harmoniously, and this current set of mechanics doesn't for all the reasons mentioned above. So the changed systems look like this:

* Classes: same as before (+open)
* Class selection: changed so that players can choose their class (+cons)
* Levelling + passives: same as before (neutral)
* Gear grinding: removed (-cons)
* Personal supply: same as before (+cons)
* Armory: more impactful and with non-random weapon effects (+cons)

This version of the game would be heavier on favoring the highly conscientious, but that's a good thing because now this happens in a more contained manner.

Before, both classes and gear grinding were things that changed the base game, now only classes do. This means that the base game is more tilted towards the highly open, but this feels coherent because it's a 30 minute max round
and you don't really have time to grind things out that much, so a mechanic that encourages grinding is in conflict with how the game plays.

Compare this to a game like Risk of Rain, for instance, which has a potentially much longer run length, and thus any mechanic involving grinding in a single run will fit it better. The time mechanic also works well with this,
since it's a pretty significant constraint that also increases difficulty, both things that the highly conscientious will like, so both this and longer runs go together and feel very harmonious.

But with SP because each round length is fairly fixed and small, you have to go for something similar to what other roguelites do which is to keep each run pure, and then add things that appeal to the conscientious outside of it.
In this case, class selection, personal supply and armory are all systems that happen outside any given match but that add predictability to it.

The armory system is the only one that you can effectively be grinded, so there's still room for an additional system that lets the conscientious feel like they're working towards something/accumulating something over multiple rounds.
Technically there already are systems which somewhat fit this, the first being the game's ranking system (normal MMR stuff) and then gold as a currency. But these feel somewhat weak, so I'd add yet another grindy system that feels
more compelling. What it would be exactly though kind of beats me, I'm not feeling like too much of an ideaguy as I write this...

Either way, that's all I wanted to say about this game's design. At all other levels of analysis this game is designed properly. Animations, shooting, driving, map design, netcode, class design, etc, everything is implemented properly
and it's hard for the find flaws with any of it. The biggest flaws are definitely in all this high level stuff that's softer and more subtle to reason about, and it would be sad to see this game not get the popularity it deserves due
to easily correctible mistakes here.

Devs will 100% not read this but still feels like a good exercise to write it all out anyway. Great game, I'll probably end up playing it for a few thousand hours if it doesn't die too quickly after release.

[Subscribe to my newsletter](https://buttondown.email/a327ex) if you want to get posts like this one in your inbox.
