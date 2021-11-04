+++
title = "NFTs, status and creativity"
tags = [
    "crypto",
    "psychology"
]
date = "2021-10-29"
images = ["https://i.imgur.com/B3srhZk.png"]
+++

I've been following crypto since 2012 and I first got interested in it mostly for academic reasons. It was an interesting development in computer science and I followed it somewhat closely for a couple of years. I feel like I have a fairly good understanding of it, but I've been really on and off about paying attention to further developments since like 2014-2015, so if anything I say here is wrong, please feel free to correct me and I'll update the post.

Essentially there are two ways to keep track of money, or of who owes who what: tokens and ledgers. Tokens directly represent the state of reality. If you have a gold coin, you have the coin. If you give it to someone else, you don't have it anymore. Ledgers indirectly represent the state of reality. Transactions are written down and the balance of each account can be derived from the transactions and their order.

In the digital world, because everything is information, we can only have ledgers. This is because if you give someone a token in the digital world, you're actually giving them a perfect copy of that token, but they can't know for sure that you'll delete your copy, since copies are easy and cost nothing to make. So tokens, as they exist in reality, are useless as record keeping devices in the digital realm.

The way people have usually solved this is through the implementation of centralized ledgers, like PayPal. Since digital information can be effortlessly copied and changed without any trace, a trusted party is always necessary for things to work like they do in the real world.

The problem Bitcoin solved was enabling the existence of a ledger that didn't need any centralized trusted party. The blockchain is a decentralized trustless ledger. It's a public record keeping device that can't be changed, hacked or stopped as long as there are participants willing to use it.

Solving this problem does one thing: it enables the digital world to have tokens. Bitcoin itself is the first token that the blockchain enabled. Now, for the first time ever, in the digital world, you can have a token that represents something, and you can send that token to someone else, and that person can be sure that you don't have an additional copy of it. This is also referred to as the ["double-spending problem"](https://en.wikipedia.org/wiki/Double-spending):

{{< figure src="https://i.imgur.com/xqUkDpj.png" >}}

That's from Bitcoin's white paper. Once you understand that this is what Bitcoin managed to achieve, to introduce scarcity to the digital world, it becomes easy to understand what NFTs are and what they will be in the future.

## NFTs

NFTs are nothing more than tokens as I have described them so far, except not fungible. A digital gold coin (like bitcoin) is fungible, the representation of ownership of a specific JPEG is not fungible. But both things are tokens. If someone sends you the token, you can be sure that they don't have it anymore. It can't be copied, hacked, etc, because it shares the same technological advancement that is Bitcoin, which is the introduction of scarcity to the digital realm.

When I first learned about NFTs, which was at the end of 2020 I think, I didn't really make the connection. But after a few months it dawned on me that NFTs were the first real step crypto had taken towards "tokenizing" the world.

Back in 2014 a lot of people would talk about how some future uses of Bitcoin would involve tokenizing things in the real world. For instance, a house or a car. If house/car ownership is represented as a token, the process of ownership transfer becomes extremely easy, since it's just about sending the token from one wallet to another. Similarly, the house/car can now act as a platform and only perform certain functions if the token of its own ownership is present (and this would generally be in your phone, for instance).

While the idea of tokenizing the world is good, there's no obvious path from Bitcoin to it. Except that now with NFTs there is. Instead of going from physical to digital, NFTs go from digital to physical, emulating what Bitcoin itself is, which is transforming pure information (transactions) into a tangible token that can be exchanged.

NFTs are also transforming pure information (currently JPEGs) into tangible tokens that can be exchanged. And while this seems kind of useless for JPEGs, this moves things closer to solving the fundamental problem faced by anyone who wants to turn physical objects into digital tokens, which is that you have to convince everyone else to agree to the setup.

You can't just say that you'll turn your house into a token if no one will accept that the token actually represents ownership of the house. But NFTs initiated the process of, let's say, conditioning the general public, into accepting that digital tokens have inherent value and can be exchanged for real money.

And once this process is complete, well, then it's only a matter of time until everything that can be tokenized becomes tokenized. To understand why this is desirable at all, let's engage in an exercise:

## How to kill Steam

As a disclaimer, I really like Valve and Steam and I would absolutely not want to see it dead. I think they provide an extremely valuable service and that their charging of 30% of your profits for this service is fair. And I also think that for a megacorp they're very forward thinking, and as indiedevs we got lucky that they happen to be our megacorp. I believe all of this unironically and I was not paid Gaben tokens to write this. However, killing Steam with crypto is a path that I can now see clearly so I won't let my pro Gaben bias get in the way of progress.

The main problem with killing Steam, and this is a problem that everyone who has tried to create their own store has faced, is creating enough momentum in your own store so that network effects make it take off and make it a viable business that can generate profits on its own and grow.

This is also referred to as the "cold start problem". Most attempts at this have failed because Steam is too powerful. It's powerful because too many users have their games locked in the platform, and the platform also happens to provide a lot of additional value on top of just being a storage facility for people's games.

One way to solve the cold start problem with crypto is by literally paying people to use your store. Tim gave people free games, but that was clearly not enough. To really get people to use your store over Steam you have to actually pay them. But how will you, an indie developer, have hundreds of millions of dollars to give away for free?

What most crypto projects enable is ownership of the company by the public via their tokens. When you look at a game like [Axie Infinity](https://axieinfinity.com/), the setup is very simple: you play the game and you can make tokens from playing. This is not conceptually different from people earning bitcoin by mining it.

Similarly to Bitcoin, early adopters are rewarded massively, as token rewards for each task are higher earlier on, and over time these tokens will increase in value as the company's value appreciates (if the project catches on, that is). This setup, of giving people a percentage of all tokens generated, costs you, the developer of the platform, nothing. All you have to do is build your project, and issue tokens (shares) of your company to the public based on them using your project.

How does this help you kill Steam? Well, it solves the cold start problem. If people are getting rich off your platform's success then that will attract more users. And if the platform is good at all then those users will keep using it. This is just a slightly more convoluted way of doing a more aggressive version of what Tim tried to do with EGS, except without needing the exclusives. Let's work out some of the details of this system.

### GameForFun

Let's say the platform is called GameForFun, or GFF in short. I spent a lot of time writing the code for this, and let's say that I've managed to match Steam in the most important features. That is, developers can upload games to the platform, users can download it, there's a storefront with all sorts of search options, there's achievements, reviews, friends, forums, etc, etc. 

This platform has a token called GFF, and I, as the creator of the platform can decide how these tokens will be distributed. As a reference, let's look at how Axie Infinity's tokens are distributed:

{{< figure src="https://i.imgur.com/9hXPaOw.png" >}}

Interesting. Looking at it now I'm actually not sure what my distribution will look like, but regardless of what it's like, I want to make sure some of the tokens always go to the node operators, who are essentially people who will be running servers that will ensure the platform works in a decentralized manner. These people would be rewarded with GFF tokens for essentially taking on the cost of letting people download games, which I assume is the most costly thing in a game platform like Steam.

Game developers would also be rewarded GFF tokens for uploading their games to the platform, and users would be rewarded for buying games, playing games, leaving reviews, getting achievements, and so on.

Over time these rewards would decrease, and other activities would start being more attractive. For instance, while initially node operators would be rewarded with the greatest amount of GFF tokens, as the platform matures and token generation decreases eventually they would be rewarded with a small percentage of all transactions that happen on the platform, which could prove to be extremely lucrative should the platform really evolve into challenging Steam.

Whenever a game developer sells his game on the platform, the game is sold as a special token. Let's call it a GFFG, short for "GameForFun game token". This is a token that represents ownership over a copy of a game. So, like on Steam, where when you buy a game you're actually buying a license to download the game on Steam, whenever you buy a game on GFF you'll be buying a token that the platform can read and that lets you download the game in it.

Unlike Steam, because this is a tangible token, it can be traded. So once you're done with the game, you could sell it to someone else who wants to play that game. And because this is a digital token and it is programmable, the game developer could decide that for every resale, 20% of the value of that resale will go back to him. So if person A bought the game for $10, and is now reselling it for $10 again, they will actually only get $8 and $2 will automatically go back to the developer. This setup already exists on current NFTs.

Developers can also set their tokens such that profit is easily shared among multiple people. Right now, if you're a team of 3 and you want Steam to send money every month to 3 different bank accounts, that's impossible. It's just not a feature that Steam supports. I'm sure they have their reasons for it, but this is easily implementable with game tokens. All you have to do is say that 33.33% of the token's value will go to address A, B and C each, and then on every sale of the token this is what will automatically happen.

Finally, because the platform is run by node operators (no server costs for me personally) and I, the creator of the platform, have already been paid in GFF tokens that will massively increase in value over time, I have very little incentive to extract money out of game developers like Steam does.

Maybe a small percentage of every transaction, like 0.1% or 1%, once the token generation phase is over, but otherwise, at least initially, because GFF tokens will be the primary form of compensation for everyone, this enables the platform to have actual zero cost. This means that every game developer using my platform is, by default, making 100% (and 99-98% eventually) of the money paid for each copy of their game, instead of 70% of it like it is with Steam.

### DevForFun

But why stop at a game store? The same exact playbook could be applied to a game engine. Everything I just described for the GFF store applies here, except that with a game engine you have a few more interesting setups possible. Imagine the Unity asset store. Assets are sold there for a fixed price, and when you buy them you can add them to your game.

What if the assets were mostly free (although some of them could also be paid) but they took a very small percentage of the profits of every game they're used in? Let's say you create models for a set of barrels. Any developer who wants to use your very professional-looking barrels can decide to add them to their engine, and the engine itself will do the job of checking when any of those assets are used in any game, and when "compiling" the game (compiling a game now involves both compiling it in the traditional sense but also creating the contract that will mint tokens for this specific game) it will be compiled in such a manner as to send the small percentage of the proceeds to the wallet of the asset creator.

So if you set the percentage at 0.01%, any game that uses any of your barrels will automatically pay you 0.1 cents per 10 dollar transaction. This doesn't seem like a lot but let's say your barrels are used in 500 games, and these games are being sold on average for 25 dollars. This means you're geting 0.25 cents per transaction. Let's say across these 500 games there's about 500k transactions per month. This means that from the barrels alone you'd be making 1250 dollars per month. And assuming that you're not only capable of doing barrels you can do the math on how profitable this could be.

And from the perspective of the game developer this makes perfect sense too. Let's say the dev ends up using a total of 200 assets, and these assets would be combinations of models, code, music, anything that makes up the game and isn't made by the dev himself. Each asset would command a different percentage based on how useful it is, but let's say that at the end of the day the 200 assets amount to a total of 10% of the game's earnings.

This means that for every $10 sale of this game, $1 of it will automatically go to 200 different asset creators who will all be getting fairly compensated for their work. And of course, they will also be getting extremely rich from getting in on putting their assets on the DFF asset store early and earning lots of DFF tokens, and so on and so forth. And everyone would win and be happy!

## World tokenization

Now imagine what this setup, when it comes about, will do to traditional stores like Steam. It makes absolutely no sense to use Steam anymore as you have a tremendous amount of incentives to both use the DFF engine and GFF store, as you're literally getting paid to do so, but on top of that, the technology that drives both of these products is actually just fundamentally better on multiple fronts.

You could also imagine that there will be multiple game stores and multiple game engines doing this same thing, but because these platforms are going to be both decentralized and public, none of them can actually lock customers in like Steam does. Because GFFG tokens for a specific game are tradeable, they will be swappable for AYNG tokens (AYNG is another decentralized game store) and, in fact, eventually the process of swapping GFFG and AYNG tokens will be seamless and it will be just like if you owned one global token of ownership for that specific game.

Decentralized game stores then simply act as readers of game tokens, and if you own the token for a specific game you can go to a store and download it. Now imagine this for every digital good. Movies, music, books, anything. Everyone who worked on any collective artistic endeavor would automatically be paid fairly for their work, and if you own a token to that piece of media you'd just be able to go to a decentralized store and access the content, because you actually own it.

Similarly, all your social media information would also be tokenizable, and you'd own it yourself, instead of it being centralized on twitter, or reddit, or whatever. And all platforms would do would be read that information and display it however they would. You wouldn't be able to get banned or deleted off the internet because you actually own the information and platforms simply have read access to it.

This is a future where, because of Bitcoin's tokenization technology, everything that can be tokenized is tokenized. And for the first time ever you actually have a path to making the Internet truly decentralized, like it was supposed to be.

I don't know how long what I described here will take to happen, maybe 10, 20 or 30 years, or maybe it won't even happen at all... But even the possibility of this future is extremely whitepilling to me and it is fundamentally why I really like NFTs.

### Example: ultra.io

I found out about this project called [ultra.io](https://ultra.io/) when [someone told me about it on twitter](https://twitter.com/DairyJohn1/status/1454262041431076865) after posting this article. This project essentially implements everything that I mentioned here and a bunch of other things as well.

This particular project seems more centralized than the imagined one I described, and the fees are also pretty high (15%) compared to what they could be, so I'm actually not too excited about it. But if you wanted a live example of everything that I described this would be it.

# Artists & gamedevs

Now for the rest of this article. So far I've described why I like NFTs. But now we must understand why others don't like it. And as a game developer it's my job to understand the behaviors of the masses at the deepest levels possible, and so that's what I'm gonna do.

It's somewhat expected that most artists & gamedevs encountering NFTs now haven't thought all that I just described through. It's expected that they don't make the connection that eventually these systems will make it much easier for them to make a living out of being artists & gamedevs.

It's natural that people reject new things that are too different or weird. But it's valuable to really dive deep into why people reject new things even after being given all the arguments and all the evidence necessary to convince them otherwise.

For instance, the 2 main arguments against NFTs are that they are bad for the environment and that they are scams. It's literally of no use to mention that many chains now are proof of stake and have negligible effect on the environment. It's equally pointless to try to argue that while scams are indeed bad, as long as you're not doing them yourself that shouldn't really affect your decisions, right? And the question you could ask yourself is, why are these arguments useless? I personally think I have a very good answer to this question, and it starts with this quote by Jonathan Blow:

{{< figure src="https://i.imgur.com/07I5JPE.png" >}}

Artists & gamedevs are given a new tool that enables them to make some good money. They don't have to be starving artists anymore. Yet most of them reply to this tool with "no". According to Jonathan Blow, it's because most of them want to be comfortable and not successful. They don't want to take risks on something new and unproven, and the thing already has a somewhat negative reputation, so why risk it. And while this is a good answer it can further divided into two concepts: status and agreeableness.

## Status

Status is the thing that anyone who's an artist or a gamedev on twitter is addicted to. I've come to think of it as interchangeable with money. Money is obviously not status, and status is not money, but they share some very similar properties and people behave very similarly around them.

Whenever you don't have any money, and you make having more money your primary goal, should that goal be reached (i.e. you win the lottery), you either need to change your goals (and that generally makes you go through a depressive period) or you just keep endlessly making more and more money for no real reason.

The exact same dynamic happens with status. If you have low status and you make having more status your primary goal, whenever you reach high status you can either go through that goal changing period or you can keep trying to get more and more status endlessly for no reason.

Because status is less tangible than money, and because rejecting money also increases your status, it's easier for people to get lost in the status grind without realizing that that's what they're doing. And in my opinion that's the state most artists & gamedevs on twitter find themselves in. 

The way this applies to NFTs is very simple. Artists & gamedevs on twitter are extremely attuned to each other's status, and they want to constantly increase their own. Whenever something low status comes along, it's of utmost importance to status attuned people to make sure that they're not in any way attached to that thing. So when NFTs come along and are attached to high energy usage, they immediately become low status, because not caring about the environment is low status.

This, naturally, leads every artist & gamedev to not want to be attached to NFTs because they don't want to be seen as low status. And once something is low status, it's very difficult to make it not low status. Pointing out that there are lots of chains that use almost no energy to work is irrelevant, because NFTs are low status already, and no facts are going to change that. So even if you release an NFT on one of these low energy chains, you're as good as dead to status attuned people, because NFTs are low status and that's that.

While this seems cynical, this is sadly how most status addicts process this situation. And obviously everyone does this without thinking or being aware of it, because these things are just built into people's bodies and it just happens automatically. But it's important to be able to identify this, because once you're aware of it you see it everywhere. Three examples (and as a disclaimer, I have nothing against the people used in these examples, they just happen to be very good examples):

{{< figure src="https://i.imgur.com/febclMe.png" >}}

Not only did this artist reject the low status thing, but she also rejected money, another low status thing. So this is double low status rejection, which means that with this tweet alone she collected quite a lot of status for herself. And you can even see how much of it was generated on the image. About 14000 of it. Crazy. Another example:

{{< figure src="https://i.imgur.com/nY3ZBvZ.png" >}}

In this case someone stole Kenney's application and then started minting NFTs with it. In theory I don't really have a problem with this situation at all, in the sense that Kenney is right in being really upset about this. But you know, the second tweet has some amount of status farming, or some would say "repfarming".

Not only did the nightmare of every artist happen to him, but he's also a really high status individual who super cares about the environment and now the low status NFT meanies came for him. This is obviously despite the fact that the chain the thief used for his crime is one of those proof of stake ones that don't really actually use that much energy at all, but, again, the facts are irrelevant because NFTs are low status.

The second tweet is an unnecessary comment, but again, twitter artists addicted to status just naturally engage in behaviors that will increase their status as much as they can. In the case of Kenney it makes sense that he is addicted to status, since he releases free things and doesn't get paid in money (remember that money is low status), but gets paid in status, and it's high quality status too, since it has the same double status buff that @castapixel's tweet has. And once you get hooked on that stuff... Very hard to stop. Another example:

{{< figure src="https://i.imgur.com/qS5mIsP.png" >}}

{{< figure src="https://i.imgur.com/WPdMxtK.png" >}}

This one is slightly less reasonable than Kenney's case because he released the thing for free, with a permissive license, except if it's used for NFTs. There's a reason why licenses are structured the way they are and why there are commercial and non-commercial licenses.

If you don't want your things to be used commercially then release it under a non-commercial license, but if you want it to be completely permissive except for one thing you don't like then that doesn't really work. I mean, you can do it, but it hasn't been tested at all in the real world so you're relying on people's good will rather than on any protection of the law.

In all these cases the same thing is apparent, NFTs are low status and thus these artists want to distance themselves from it as much as possible. But not only are they low status because of the environment, but also because of money. Artists in general view making money itself as low status, so this is yet another motivation for disliking NFTs.

Why is it useful to look at things like this? Because you can't escape from it. I also have a status monkey inside me that constantly wants more status and importance and attention, and I can't really turn it off. It's built-in human behavior.

But you can at least know that it exists, pay attention to it, and pay attention to how it makes you change your behavior. Often times your status drive can be an extremely good and productive thing. But often times it can lead you down endless holes of self-sabotage and despair. It's up to you to understand that it exists and to try to control when necessary.

Any artist or gamedev that is controlled by his status drive is likely not going to produce truthful art. They will produce art that makes their status monkey happy. And while occasionally the monkey might produce something good, more often than not it will just throw shit all over the walls.

## Agreeableness

Agreeableness is the personality trait that refers to how compassionate, caring, and overall empathetic someone is. People who are agreeable are team players, they will more often sacrifice themselves for others, and most importantly they really like avoiding short/medium term conflict. They don't like engaging in those kinds of contentious situations often and they prefer to diffuse them as much as possible.

{{< figure src="https://i.imgur.com/2t5aH7s.png" >}}

Women are generally more agreeable than men, as the graph above shows, but the average difference is not that big. If you picked a random man and a random woman, 60% of the time the woman would be more agreeable, which really is not a lot. And agreeableness is one of the biggest personality differences between men and women, so when people say that men and women are temperamentally a lot more alike than people assume that is somewhat true.

However, when you start looking at the edges of the distribution the differences start becoming more clear. If you tried another exercise and picked the most agreeable person out of 100, 95%+ of the time that person will be a woman. Similarly, if you picked the most disagreeable person out of 100, 95%+ of the time that person will be a man. This is why, for instance, most people in prison are men, since high levels of disagreeableness essentially means you don't care about the law nor about hurting other people.

The main pros of high agreeableness are obvious, the cons of high disagreeableness are obvious, but people generally don't understand either the cons of high agreeableness or the pros of high disagreeableness. One of the main cons of high agreeableness is that highly agreeable people have a really hard time saying "no". For instance, I don't need to know anything about the game below to guess that the authors are likely women who are going through the process of becoming more disagreeable:

{{< youtube Kf7YrsMR2ws >}}

The path in life for agreeable people is one of becoming more assertive and learning to do things like saying "no" more often, because if you don't do that you're just a pushover and people will definitely notice it and take advantage of it, especially more disagreeable people.

This feeds into another downside of high agreeableness which is the avoidance of short/medium term conflicts. The reason why agreeables don't like saying no is because fundamentally they don't like being in situations where they are in conflict with someone who they believe to be a part of their ingroup.

They have absolutely no problem being in conflict with those that are a part of their outgroup. In fact, one common mistake agreeable people make when becoming more disagreeable is incorrectly identifying people as part of their outgroup so they can avoid feeling bad about being in conflict with them, but this is generally counterproductive because most people are not a part of your outgroup, certainly not in a work environment, for instance, and when you treat people as if they were you generally are way more aggressive than necessary. So there's this really hard balance to strike between just standing your ground and being more assertive while not being outright aggressive in a way that doesn't make sense.

In any case, the problem with avoidance of short/medium term conflict is that those kinds of conflicts are good. People who are well adjusted in terms of agreeableness will go through many small conflicts with each other and will set up and dismantle borders around them constantly until they're fine with each others presence and they can co-exist peacefully.

If you don't go through this process with someone and you don't communicate to one another what your actual borders are because you want to avoid conflict, then small disagreements tend to bubble up, and given enough time they eventually blow up in a really unnecessary way.

It is extremely common to see this with any kind of drama that makes its way to the internet, especially on twitter. I happen to be somewhat of a drama connoisseur, (if you couldn't tell I really like psychoanalyzing groups of people) so whenever there's any kind of gamedev related drama, from GamerGate to people unfortunately killing themselves because they got cancelled, I tend to pay attention.

And whenever you read through these situations, and generally the people involved will make very long posts about it describing everything that happened, 95% of the time none of the problems would have happened if the people involved were just more assertive and less agreeable. It's really striking how this process I just described happens, where small things don't get resolved because people want to avoid conflict, and then these small things evolve into these huge issues that eventually have to explode in one way or another. All of it completely unnecessary.

Now, why is knowing all this important? Because you can explain a lot of group behaviors with agreeableness alone. Most artists and gamedevs using twitter are highly agreeable people, and once you understand this and what it entails you can very easily predict how they will respond to all sorts of different situations. Like NFTs. Once NFTs get enough of a bad rep it's pretty much a given that every artist and gamedev with above average levels of agreeableness will want nothing to do with it, because they don't want be in conflict with their audience and with their peers.

The negatives of NFTs, when it comes to agreeableness, are that the space really does have a lot of scams going on. To an agreeable person it's unacceptable that someone would involve themselves in this as it's a breeding ground for really morally dubious behavior by so many people.

But to a disagreeable person (like me), as long you're not doing anything immoral yourself, you're not stealing from anyone and you're not buying things that are stolen, then there's no issue. It's just new technology and new technology will always be used by thieves and scammers first before it becomes more useful to the general population.

But agreeable people can't think like that. They can't ignore an artist they know getting their art stolen because they are too compassionate. So what will happen is that they will more easily cast *everyone* who engages with NFTs as part of their outgroup, regardless of if the person is doing anything immoral or not, and the rest naturally follows.

Having all that said, both status and agreeableness are the main reasons why I think so many artists and gamedevs on twitter reject NFTs from a more fundamental standpoint. And because both of these things are deeply rooted in people, you can't really change it or convince people with arguments. However, I do think that most agreeable artists and gamedevs are at a fundamental disadvantage when it comes to being creative individuals because

## Creativity and disagreeableness

To be creative you have to be open to new experiences. This is a trait that refers to your ability to think outside the box, to make connections between things that weren't previously connected, to break down borders and mix and match things so that something new emerges out of it. Pretty much everyone who decides to make games is higher on openness than the average person.

One way you can see this clearly is in the phenomenon of gamedevs who can never finish a game. To finish a game you have to stick to the same project for a longer period than you might want, and you have to resist the temptation to go for a new idea. For highly open people, "new" is always a big motivator, and so whenever a game gets to that middle period where it's mostly a grind, "new" becomes ever more attractive and it makes people drop their games without finishing them.

As an aside, something else that follows from this is that certain drugs, like psychotropics, *increase* your levels of openness permanently, as mentioned in the video below:

{{< youtubestartend 35e5i6FQuMw 232 >}}

What this means is that if you're already highly open, and you have trouble finishing games, you definitely don't want to take any psychotropics because they will increase your openness levels even further which means you really won't be able to stick to anything for any reasonable period of time. Now, if I had to guess, at least 50% of artists & gamedevs have already done those drugs at least once, so that would explain a lot of trouble people have with finishing games in the first place. So don't do them if you haven't already!

In any case, to be creative you have to be open, OK. But another trait that helps is also being disagreeable. The role of a creative individual is creating things that haven't been created before, right? It's making connections that no one has made, it's bringing forth new knowledge from the vast unknowns. That's what moves society, that's what has enabled us to prosper as much as we have today.

But to successfully do that you have to be willing to be wrong, and I mean really wrong, a lot of times. Anyone who cares too deeply about not being wrong, either because they're too agreeable or because they care too much about their status, is not going to be able to be usefully creative because the things they create will often be too safe.

Their creations are within the bounds of what's acceptable, and so they can't truly innovate in ways that creatives should be innovating. This applies not only to the arts, but also to science:

{{< figure src="https://i.imgur.com/xwpGoAp.png" >}}

What this means when it comes to crypto and NFTs is that, in my opinion, they're a field with a lot of truly creative energy right now. It's where a lot of new things are happening and where the unknown is being brought forth to fundamentally change things. You can tell this is the case because people still don't understand what NFTs are or what value they have. Any idea that is immediately understandable by everyone isn't truly new, so at the very least we can tell that NFTs are, in fact, *new*. If they are useful or not that's up to time to decide.

What is important is that if you're a creative person you should understand that this is how creatives work. They create things that might be tremendously wrong, but that might also be tremendously right. No one knows which is which until it's obvious and then in hindsight people say that they knew it all along. So if you want to be truly creative, you need to be willing to be tremendously wrong, otherwise you're not really creating that much value. Another way of putting it is [like this](https://twitter.com/jmrphy/status/1445473664460226561):

{{< figure src="https://i.imgur.com/2cFflcq.png" >}}

{{< figure src="https://i.imgur.com/7XzlbPC.png" >}}

Can creatives who are extremely agreeable and care a lot about their status still be successful in their fields? Absolutely. Gaming especially is a constantly growing field, so to be successful you don't really have to innovate that much.

But if you want to aim higher and try to really be usefully creative as much as you can, and to occupy the role of a creative in society as much as you can, creating as much value as you can, then you can't really be too agreeable nor care too much about your status. You have to be willing to be wrong, to look stupid, to be a clown, and to be cringe. Only when you're willing to let that happen will you be able to find valuable things that no one else can because you're constantly looking where no one else is.

[Subscribe to my newsletter](https://buttondown.email/a327ex) if you want to get posts like this one in your inbox.
