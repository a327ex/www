+++
title = "Skill death spirals"
tags = [
    "design",
    "skill death spiral",
    "luck",
]
date = "2022-09-09"
images = ["https://i.imgur.com/CiKMPfX.png"]
+++

Recently I've been playing [Rumbleverse](https://www.rumbleverse.com/en) a lot after watching [NL](https://www.youtube.com/channel/UC3tNpTOHsTnkmbwztCs30sA) play it
and also because I need to somehow fight my Super People withdrawal, and it's a very fun game. However, playing it has made me think more and more about a problem I've mentioned in my 
[past two](https://www.a327ex.com/posts/super_people_test_session/) [Super People posts](https://www.a327ex.com/posts/super_people_final_beta/), which is the problem of the "skill death spiral".

This is a problem every competitive multiplayer game has to manage somehow, but it's especially problematic with BRs because they uniquely need a very high population of players so matches can start in a timely manner,
which means that they're more sensitive to the problem and thus are the best games to use for its analysis.

## Description

In a BR, players of varying skill levels are matched together out of necessity. If the game's mechanics reward skill too much, more skilled players will consistently beat lesser skilled players.

When you put these two facts together you get a situation where more skilled players consistently dominate lobbies, which means that they're the ones having most of the fun at the expense of all other 
players who die early and often.

The further away from release date the game is the more this effect is pronounced, as the biggest and first generation of players has had more time to learn the game.
This means that the more time passes, the less welcoming the game will be to new players as they will be more likely matched against first generation players.

All of this results in a death spiral in regards to the game's population. First, new players will quit earlier and more often since they will rarely be having fun.
Second, skilled first generation players who don't play as much or don't learn as fast will also eventually start quitting, as even higher skilled other first generation players will consistently dominate them.

If nothing is done, this process repeats itself until the game's population has completely stopped playing. It's a death full of *very* high skill lobbies, but it's a death nonetheless.

## Luck and TTK

One of the most effective ways of reducing skill death spirals is by introducing luck to the game's design. This is described well in this clip:

{{< youtubestartend dSg408i-eKw 1548 >}}

In a BR with 60-100 players of varying skill levels and where the most skilled players consistently win, those more skilled players are getting all the fun the game generates and leaving none of it for other players.

You can think of "fun" as a resource the game generates, and your goal as a designer is to make it so that the [Gini coefficient](https://en.wikipedia.org/wiki/Gini_coefficient) of fun distribution is not very high.
You want lesser skilled players to be able to occasionally kill very skilled players, since if that doesn't happen then a skill death spiral will start developing.

The video above uses TF2's addition of crits as an example of introducing luck to a game's design and it immediately feeling more fun to players. For a BR like PUBG or Super People you could also add more luck by 
adding crits, but you can also do it by decreasing TTK. If the time it takes to kill a player decreases, it means that players getting caught off guard will have less time to respond.

This seems like it punishes new players more than it does skilled players. After all, who likes getting killed in 1 hit from 300 meters away without even being able to see the attacker?
But you shouldn't look at the problem from an individual player's perspective, but rather from a "what happens to all lobbies" perspective.

And what happens to all lobbies is that more skilled players will die more often and earlier with lower TTK than with higher TTK. If more skilled players die more often and earlier, "fun", the resource, is able to
be distributed more often to other players, who by sheer numbers will be more likely to be less skilled.

This is counterintuitive. You would think making individual encounters *more* punishing would make the game *less* welcoming to new players, but the success of BRs with low TTK and the relative lack of success of BRs with high TTK
shows the opposite might be true.

This dynamic also becomes obvious if you play any of these games a lot. When I wrote my [second Super People post](https://www.a327ex.com/posts/super_people_test_session/) going over the lower TTK changes the devs made to that 
test session, I had been playing Super People for 10-12 hours every day for the past entire month, so I was *very* attuned to how the game felt.

And the difference in behavior from players who were more skilled than me, as well as the way I had to change my behavior so I would die less often to players who were less skilled than me, was obvious.
More skilled players were simply less capable of getting away with as much as they could before, which made it less likely for them dominate lobbies, and also made it more likely for them to die earlier if they failed to play
more conservatively.

So this is just one of those things where even though it is counterintuitive, it seems to be true to me. Of course, lower TTK is not the only thing that can increase luck in a game, but it's the most general thing that everything
reduces to. For instance, TF2's crit addition (assuming nothing else was changed) was essentially a TTK decrease, since crits existing increases overall DPS and thus reduces TTK.

## Disengagements

Another thing that contributes to death spirals is how easy or hard it is to disengage from combat. Lower TTK means disengagements are harder since engagements tend to be more deadly, so it must follow that hard disengagements
decrease the effects of death spirals, while easy disengagements increase it.

If you play these games it's also obvious how this is true. If disengagements from combat are easy, skilled players can play way more aggressively since they know if things go south they'll have time to disengage, heal,
and then come back. This means that it will be easier for them to dominate lobbies, which means that the effects of a death spiral will be more pronounced.

In shooting BRs like PUBG or Super People I'd say disengagements tend to be somewhat difficult. If you're really far away from the other player you can generally disengage safely, but otherwise you're stuck until your opponent is dead.
This is compounded by the fact that every time someone shoots in one of these games (without a silencer), it attracts third parties who want to see what the shooting is about.

At least that's how I play it and how most other skilled players also do. If I hear shooting somewhere, I'm moving towards it to assess the situation since often times you can get free kills, and thus loot, out of it.

A game like Rumbleverse on the other hand has extremely high TTK and extremely easy disengagements, both things which benefit more skilled players above everyone else.
However, Rumbleverse also has extremely easy engagements.

Because TTK is so high and disengagements are so easy, people are way more likely to engage in combat since it costs less, and thus increase the game's overall randomness/luck.
This effect is a lot more noticeable in duos than in solos, so if I had to make a wild guess, relative to each other, Rumbleverse's duo queues will die slower than its solo queues.

## Match duration

Match duration is also a consideration, given that shorter matches directly result in faster queues, which stave off death spirals.
PUBG and Super People have a somewhat high match duration, while Rumbleverse's is significantly lower.

The amount of players per round also matters, since lower players per lobby also results in faster queues. PUBG has 100 player lobbies, Super People has 64 player lobbies, and Rumbleverse has 40.
So even though Rumbleverse's death spiral problems are bad from a TTK/disengagement perspective, they're made better comparatively by its smaller player number requirements as well as smaller match duration.

The only negative effect of shorter matches, and this is something that I noticed in myself only, but I suspect it also applies to lots of other people, is that it's way easier to play the game in shorter bursts.
When I play Super People I make sure that I'll have a block of 3-4 hours to do it because playing one match and then stopping just feels incorrect given each match's duration.

Whereas with Rumbleverse, playing one or two matches is something that you can do in like 10-20 minutes, so it feels much easier to say "let's just play some Rumbleverse quickly and then go back to what I was doing".

You can also look at this from a perspective of: how many times per hour does the game give you the option to quit?
In a game like Super People where each match takes like 30-40 minutes the answer will be 2-3. Whereas for Rumbleverse where each match takes like 10 minutes, the answer will be 6+.
Naturally, the game that gives players more options to quit per hour, will have more players quitting per hour.

## Matchmaking queues

Dividing matchmaking queues between multiple game modes, such as TPP and FPP for shooting BRs like PUBG and Super People, is something that naturally helps a death spiral develop, as it cuts the game's population
into multiple queues and thus increases matchmaking duration.

For the TPP vs. FPP debate this is likely a reasonable decision, since w\*sterners are babies and can't handle playing the game on hard mode (TPP), so adding an easy mode to appease them adds hugely to the total number of players
the game has, even though ideally this divide shouldn't happen.

## Streaking

Another way to sort of see how much luck a BR has is based on how easy it is to go on winning streaks in it. One of the best Super People players I've seen on twitch, [cleansky226](https://www.twitch.tv/cleansky226), is a great
example of this.

Before the TTK reduction he was able to win easily and seamlessly most of the time he played, and after it he still wins fairly often (after all he's really good), but it's significantly less often than before.
And his deaths are usually the kinds of deaths you'd expect out of this scenario, they're these random events that he could have avoided if he played more conservatively, but playing more conservatively is kind of boring
so he doesn't do it.

If you compare it to something like Rumbleverse, on the other hand, it's a lot easier to go on winning streaks there I've both gotten a few short win streaks myself as well as seen multiple streams of people going on longer ones
and overall just having pretty crazy W/L ratios.

## Bots

Everyone knows by now these games have bots made by the developers, both to ease new players into the game, but also to fill lobbies whenever there aren't enough people playing.
What most people don't realize I think is that (and this is a huge speculation on my part, but I can't really see how it isn't true) there are two types of bots: the obvious ones and the hidden ones.

The obvious ones are bots that everyone can easily go "yea, that was a bot". They serve as a focus point for people's attention and for people's bot detection senses. "This is what a bot acts like", everyone thinks, as
they kill an obvious bot.

But there are also other bots that are not obvious at all and that act entirely like real players. These are the hidden bots, and they're hidden so well both because they act more like players, but also because people's
bot detection senses are focused on how the obvious ones behave.

I don't really have to have any evidence that this is happening simply because building human-like bots for these games doesn't strike me as the hardest of problems to solve,
and if that's the case then developers have every incentive possible to do it. Maybe I'm wrong, but I don't think I am.

We could rank different types of BRs to see how easy it would be to build a bot for them. For instance, the easiest game would probably be something like Fall Guys. All the bots have to do is run forwards and avoid obstacles,
which really doesn't seem that hard at all to code. Another very easy game (although not a BR) would be something like Super Auto Pets, as in that case you don't even need to build any kind of bot at all, you can just build fake
teams on the fly and have real players battle those.

The hardest types are probably the full featured shooting types like PUBG and Super People. These games have quite a lot of mechanics and moving parts, so getting human-like behavior in them
seems like a harder coding problem if you were to use "normal" coding, but I don't see why something like some kind of neural network approach wouldn't work here. You have all the data you need for human-like behavior
from real players, and you could probably train a model and get reasonable results by telling it to mimick that behavior on average.

In any case, the way that this helps with death spirals is obvious, as it prevents matchmaking times from getting too long, and also distributes "fun" more fairly, as the bots won't be set to be the best players in the server,
but merely to act human-like in an average way.

As is evident with TF2 (a game infested with bots), it's also trivial for bots to inflate concurrent player counts, so you can't rely on [Steam Charts](https://steamcharts.com/) or other similar tools to try to assess the "real" 
health of the game when it comes to player numbers. All of this to say, the technology is there, the incentives are also there, so it's more than likely happening.

## Super People & Rumbleverse

Now that I've gone over most of the points of analysis for skill death spirals I want to make a comparison between Super People and Rumbleverse, since these are the two BRs I've played recently
and they are also recently released games, so seeing how both of them perform over time relative to one another will probably be a good test of my "skill death spiral" theory.

### TTK

Super People has very low TTK, and thus has a higher luck component to it.
Rumbleverse has extremely high TTK, to the point where you have multiple lives, and so it rewards skill quite a lot.

This is extremely visible if you play the game, as often you will encounter someone who is either obviously less or more skilled than you, and there's nothing that can really be done to change the outcome
of the battle. The more skilled person always wins.

This would predict a stronger skill death spiral for Rumbleverse than for Super People, and if this aspect (TTK/luck) is the one that has the most importance, then the difference in results between both games should be large.

### Match duration and size

Rumbleverse has very low match duration and low requirements on player numbers per match when compared with Super People, which should offset some of its problems when it comes to TTK/luck.

And while it's easier to quit Rumbleverse more often than it is for Super People, it's also easier to play matches more often in a non-committal manner, so I wouldn't say that the negatives of shorter matches matter much here.

### Matchmaking queues

Super People has a total of 6 queues: TPP solo, TPP duo, TPP squad, FPP solo, FPP duo, FPP squad; while Rumbleverse only has 2: solos and duos.
This is a clear advantage for Rumbleverse, which is further augmented by lower match duration and match size.

### Bots

It's easier to build human-like bots for Rumbleverse than it is for Super People, but assuming both games have them then neither game particularly benefits from it more than the other.

The main difference between both games is that Rumbleverse is on the Epic Games Store, while Super People is on Steam. And despite Steam Charts not being reliable when it comes to assessing game health,
if the data is available at all people will use it to decide on whether they should play the game or not.

This can be good if the game is popping off and becoming really successful, since its very public success will attract more players, but it can also be bad and lead to a strong death spiral if player numbers
start dropping too much. None of this is a concern for Rumbleverse, since there's no Steam Charts equivalent for games on EGS.

### Fun

Is either game significantly more fun than the other? Rumbleverse is taking a lot from fighting games but it's in many ways also a fairly casual game.
It's easy to just pick up and play, it's not very punishing due to high TTK, it's easy to get in and out of fights and thus it's easy to just be constantly hitting people left and right.

Super People is slower, each match takes quite a lot longer, individual battles are very punishing, and there's a lot of downtime where you're just looting and nothing is happening.
I can see a clear argument for how Rumbleverse appeals to a higher number of people and thus is the more fun game.

However, despite Rumbleverse feeling less punishing due to high TTK, that feeling is superficial and the game is actually *very* punishing. Like, I've been playing for a week now
and I think I got pretty good at it. Sometimes I'll go on a few win streaks even. And it's just brutal the way you can consistently play around with and kill players that are less skilled than you.

I honestly feel kinda bad when I do this to other people and I feel like I'm contributing to the games eventual downfall, because it's just pure evil. And similarly, when you encounter someone more
skilled and that becomes obvious after they read you like 3 times in a row, then there's literally nothing you can do other than run away. This dynamic just feels so overwhelmingly important to me that 
I can't really ignore it.

### Summary

So to summarize, here's what the analysis looks like based on which game does it better from a skill death spiral prevention perspective:

* TTK/luck: Super People
* Match duration and size: Rumbleverse
* Matchmaking queues: Rumbleverse
* Bots: neutral, maybe a slight edge to Rumbleverse
* Fun: neutral

And so from this you could say that Super People wins on TTK/luck alone while Rumbleverse kinda wins on everything else. And this is why this comparison is so useful, because to the degree that this little analysis is true,
it means that depending on how each game performs over the next 6 months to 1 year, I can get a more clear idea on which aspect matters more for BR skill death spirals.

The possible outcomes are the following:

1. Super People succeeds and Rumbleverse fails 
2. Rumbleverse succeeds and Super People fails 
3. Neither game succeeds or fails too much and they just sort of survive
4. Both games fail

4 is the least interesting one. 3 is probably the one with the highest chance of happening. If 2 happens then it means that match duration/size, queue amount and combat heavy fun weigh more than TTK/luck when it comes to
preventing skill death spirals. And if 1 happens then it means that TTK/luck matter more than anything else when it comes to this problem.

The only issue going into this is figuring out how Rumbleverse is doing, since there's nothing like Steam Charts to use. Using streamers/youtubers as a proxy for this is a bad idea (you'd be surprised how many copies SNKRX still sells
each month despite pretty much no streamer or youtuber playing the game since like August last year), using things like twitter mentions, subreddit activity, and so on is better, but it's still kinda noisy. PUBG is the most popular
game ever and you wouldn't be able to tell that based on its subreddit, for instance.

I think ultimately the only real way to tell is if the devs stop releasing updates to the game. Every game experiences a constant drop in player numbers, and the games that manage to survive do so via updates, so this seems
like the correct data point to look for when assessing a game's health if you have no other info.

So yea, now it's just a matter of waiting and seeing. I'm personally going to play Super People over Rumbleverse because I just like it more, but hopefully both games do well. It's actually quite an interesting set of solutions
that the Rumbleverse developers settled on for their game when you compare it, for instance, with Battlerite Royale, which had a similar premise (skill heavy melee-ish combat) but went in another direction entirely.

## Is it even a problem?

To end this post, an argument could be made that "skill death spirals" aren't a problem. More skilled players *should* consistently beat lesser skilled players and as designers we shouldn't give in to people's worst impulses
and try to somehow make the game easier/rewarding for people who don't deserve it.

This starts getting into the [difficulty and accessibility](https://www.a327ex.com/posts/cons_compassion/#difficulty-and-accessibility) argument, which is a fine argument to have in general. But in this particular
situation, that of a competitive multiplayer game that has to survive for as long as possible, it seems more pragmatic to not take the Dark Souls side of it and to cater to less skilled players because you simply need to.

If you don't do this your game has a higher risk of dying, and you don't want that, so you have to do it. Of course, you should do it tastefully and carefully, but it should be done regardless.
And after the game's population has matured you can also decrease these measures and make the game reward skill more, as Richard Garfield mentioned in the video I linked earlier:

{{< youtubestartend dSg408i-eKw 1700 >}}

Many games are designed from scratch to solve this problem. For instance, I believe that the success of 5v5 in the past decade+ has largely to do with this. 1v1 games are too punishing, skill gaps are too visible,
people have no one to blame but themselves, so those games gradually become less popular.

On the other hand if you're playing with 4 other people it's very easy to blame them when you lose, but it's also more likely that someone in your team will carry you to an undeserved victory.
So 5v5 games are softer types of games with a less punishing learning curve, and that is reflected in their huge success relative to other types of multiplayer games.

Again, you could look at this and make the argument that as a designer it's your moral duty to challenge people and to help them become the best version of themselves, so purposefuly designing
games in a way that gives them outs like this is wrong.

And that would be a fine argument to make, but, you know, people are different. Some people have a pretty high resistance to harsh learning curves and enjoy the challenge, others need to be eased into it a little more.
And so if you can make a game that appeals to the latter group while antagonizing the former as little as possible (and I think adding luck achieves that well enough), then you should do it.
