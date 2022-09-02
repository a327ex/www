+++
title = "Thoughts on Super People's test session"
tags = [
    "design",
    "super people",
]
date = "2022-03-14"
images = ["https://i.imgur.com/AKSEJnM.png"]
+++

This past weekend Super People's devs ran a [test session](https://store.steampowered.com/news/app/1190340/view/5242758619715438848) aimed at seeing how TTK changes and the removal of crafting would affect the game:

{{< youtube 4HY6zKYKALc >}}

In my [previous post](https://www.a327ex.com/posts/super_people_design_review/) I went over the game's design and outlined a few things I'd change to likely improve player counts, and they were mostly focused around
removing conscientiousness-oriented mechanics from the game itself and adding them to the metagame that happens between rounds instead.

The devs ended up removing crafting, which is good, but they also decreased the game's TTK. I initially thought higher TTK was a good thing:

>As an aside, one thing that some people really don’t like about SP is that it has a higher TTK (time to kill) than most BRs, certainly higher than PUBG. But this, again, is a necessary change due to the addition of classes.
If everyone has passives and ults and whatnot, it would feel really bad if you got instantly killed without having even a chance to defend yourself using your abilities, so the higher TTK fixes this problem.

But the changes from this test session have convinced me otherwise. One of the things that happens when TTK is lower is that it's easier to kill, but it's also easier to die. In practice, this means that it's easier to die
to ambushes, to campers, or to someone who just happens lands a couple of really good shots on you.

What this does is that it adds randomness to the game. One of the problems the game had was that it was very easy for skilled players to pretty much never die. If you knew what you were doing, whenever you found yourself
in a bad spot, you'd have enough time to back away, heal, and then engage again. This meant that skilled players could play pretty aggressively without getting punished too much, and it'd lead to these players very consistently
getting 10+ kills every match, especially the shotgun masters which rely on this more aggressive playstyle.

With lower TTK this changed pretty dramatically. Quite a few players who I know are really good and who used to terrorize me are now forced to play less aggressively because they can't get away with as much as before,
and thus what happened is that they would make it to the final circles less often and with less kills than before.

This is a pretty good instance of how luck affects a game's design, an effect which has been described here:

{{< youtubestartend dSg408i-eKw 1548 >}}

In a battle royale, with 60 players, what ends up happening is that people of all skill levels are matched together, and if the game rewards skill too much then only the more skilled players end up having fun, while everyone else
just keeps getting killed over and over. You can think of "fun" as a resource that the game generates, and your goal as a designer is to make it so that the [Gini coefficient](https://en.wikipedia.org/wiki/Gini_coefficient) of fun
is not very high. 

You want lesser skilled players to be able to occasionally kill very skilled players, since if that doesn't happen then over time lesser skilled players will leave and you end up with a dwindling population of very skilled players,
who eventually will also leave because a BR needs thousands of concurrent players to work otherwise you can't find matches.

This is what happened to one of my favorite BRs, Battlerite Royale:

{{< youtubestartend Rg3MQUWNTpg 310 >}}

At the end of this video the author mentions that the BR version of Battlerite failed because it was paid, or because they broke their promises to the existing fanbase. This is the same as people saying that Artifact failed
because of the payment model. It's perhaps the most visible part of the failure, but it's not the actual reason.

Many games have been released with worse payment models or broken promises, but they still managed to succeed. If the game is actually good, *it will succeed*, regardless of whatever is happening around it. So all of these games
failed because they weren't good enough, and the way in which they weren't good enough is that they simply didn't cater to new players as much as they should.

The more tasteful way of catering to new players is with randomness, because it's something that skilled players can still work around without it feeling too unfair, and in this case with SP the TTK change perfectly achieves this,
as it increases the chances that more skilled players will be caught offguard by their lesser peers and thus keeps newer players playing for longer than they otherwise would.

---

And now for other changes. In my previous post I also mentioned that the removal of crafting should be offset by the addition of conscientiousness-oriented mechanics outside the game, namely letting players choose their classes
instead of it being random, and making the armory more powerful and less random. If I had to focus on one of them I'd definitely focus on classes not being random, as this is easily the one that will mess up new players the
most, but I already made the argument for this in that post so I won't repeat it here.

Finally, some small adjustments I'd do regarding drop rates. While crafting grind was removed, capsule grind wasn't. Finding capsules is still too grindy/hard and should be easier, especially on earlier levels.

Along with this, due to the removal of Lv.1 gear from drops, now it's a lot easier to go without finding armor/helmet for long periods of time. One match I spent like 10 minutes looting without finding neither armor nor helmet and
only was able to get them after I killed someone. One easy way to solve this is to increase the drop rate for Lv.2 gear/helmet, but another more permanent way that also fixes the capsule issue is to enforce drops for certain items
per location.

You could look at a BR map as a graph. Each location that can spawn items is a node that's connected to neighboring nodes. To ensure that you can't go too long without finding gear/helmet/capsules, you can run some code
on this graph to ensure that at least one of these items exists every *N* nodes. Or you could divide the graph into clusters and run the constraint code for each cluster. You could also integrate node distance into this,
since for rural areas nodes will be fairly spaced out from each other, meaning that you'd need the number *N* or the cluster size to be smaller or larger depending on node density as measured by node distance.

Some fairly small changes but they were noticeable enough to be worth of a mention. In any case, lower TTK was an interesting and surprising thing that I didn't realize was so important for this game, but that now seems obvious.
Overall I'm fairly happy with how this game is going and the devs seem to be on top of things, so hopefully it does well once it releases!
