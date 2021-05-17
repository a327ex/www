+++
title = "Lessons learned from releasing my second game"
tags = [
    "indiedev",
    "postmortem",
]
draft = true
+++

[SNKRX](https://store.steampowered.com/app/915310/SNKRX/) is the second game I've released on Steam and in this post I'll go over my thoughts on its development.

For context, I made this game in the past 3 months as an ongoing dev challenge I have with myself to start making games more consistently every 2 months or so.
I'll divide the contents of this post in 4 sections: programming, design, strategy/business and a more general section for things that don't fit the others.

<!--more-->

# Programming

## Engine

### Unchanging code

Since about the middle of last year I've made it an explicit goal to change my engine code as little as possible between projects.
Before then, whenever jumping around projects I would try to do things a different way to see if that way was better.
Be it 0% OOP, 100% OOP, ECS, event driven, whatever. I've tried lots of different high level concepts for organizing engine code. 

Basically this would lead me to rewriting some of the common code between projects in these different ways and that would end up taking some time and effort.
I was fine with it because I was mostly exploring but at some point I'd had enough of it and decided to just settle on one way of doing things.

This settling was helpful because very quickly after it I was getting more done faster than ever before, and with each failed project,
instead of taking nothing but experience from it, I was also taking artifacts, since each different project would require a few different engine level functions or modules,
and I would also make sure to document those well enough that they could be reused in the future. 

### Artifact accumulation

This changed my mindset from one of "premature generalization is bad" to one of "artifact accumulation is good".
Basically everything I code for a project now, no matter how small it is, I'll try to see if it can be made into reusable code for future projects. 
A lot of it tends to be very specific so it can't, but often times when building something in one game there's a very clear path for how that could be a generic system that actually would work well in other projects.

One good example of this is what I call a "Nodemap".
BYTEPATH had a really big skill tree in it and the way I developed that was basically to just have a [huge table defining the skill tree](https://github.com/a327ex/BYTEPATH/blob/master/tree.lua).
This table is then fed to the game which creates the appropriate objects (nodes and edges) out of it.

For the game before SNKRX (which I dropped because I went over the 2 month limit with no real end in sight), I was doing both a skill tree and an overworld map thing,
something like Slay the Spire's map for choosing the next arena. It turned out that the code for both systems was very similar, since they're essentially graphs with nodes and edges and
rules saying that you can't go to the next node until you've cleared a neighbor.

So I've abstracted this out into a more generic Nodemap class that I didn't quite get to use for that project nor for SNKRX, but that I'll make use of for a future one for either a skill tree or an overworld map.

This kind of artifact accumulation has been happening for me since last year and it's been generally very useful, especially since I've been careful about
documenting each of those systems a lot, as I know that I intend on using them for a very long time.

### Lua frameworks

In general I've been pretty happy with Lua being my language of choice for games, as well as with LÖVE as a framework.
They both mesh together pretty well with how I like to do things and they give me enough freedom to reach the conclusions I need to reach at my own pace.

I would love for there to be some competition in the "Lua framework" space, especially one that works well with the web. 
There are plenty of Lua engines that work well with the web but I'm generally put off by engines because they constrain me too much.

I've been very inspired by [Amulet](http://www.amulet.xyz/) lately which is a Lua framework that fits the bill and it has a lot of good ideas,
but I've never managed to go beyond a few small prototypes with it because it's lacking quite a few features I've grown accostumed to.

It's the kind of thing where I know what "better" looks like: something that has LÖVE's API and most of its features, that works 100% on the web, that is also Lua based, and that has easier C/C++ integration
so that adding modules in those languages is a workflow supported by the framework itself. [LÖVR](https://lovr.org/) gets most of these things right,
unfortunately it's very focused on 3D and I haven't played around with it enough to see how feasible it is to use it for 2D projects.

The framework could also be C based, since I can just write the Lua bindings myself. There are lots of C frameworks, but their main problem is that because they're being written
in C it's rarely the case that they bother to make the API nice and easy to use like LÖVE's. In general I'll have to deal with OpenGL type of code (I don't want any of that) which defeats the purpose of the thing.

In any case, LÖVE works well enough for most things and I've gotten used to it for long enough that 
it would be mostly a waste of time to try to redo it or get used to another framework/engine. LÖVE's web export is kinda buggy but it mostly works, the features
it has are very complete, especially the graphics end of it, and while integrating C/C++ modules can be annoying it's also not really hard for the most part, and so... it just... works.

### Sticking with what works

In the [previous post](https://github.com/a327ex/blog/issues/31) I made like this I had a lot of really hot opinions about many things, but one of them was pretty much
my argument for making my own engine and how it would be great, and how Unity sucked, and all that. 

About 2 months after writing that post I managed to make a fairly OK initial version of the engine I wanted, and then 2 months llater I realized that everything I wanted to fix about LÖVE was actually
fairly doable without having to rewrite most of LÖVE in C, meaning that I could fix most of my problems with LÖVE without having to replace it.

But more importantly, LÖVE actually has a lot of graphics features that I would have to reimplement, and it turns out that I REALLY didn't like doing low level graphics code at all.
So I just decided to go back to it, fix the things I wanted to fix with my new-found knowledge and then move on. It was a very fast and useful lesson about the actual value that the framework was providing
me which was somewhat mistated when I wrote that post.

Now 3 years later, after watching the engine vs. no engine debate evolve over the years and noticing how it went for me,
I'd say that for the most part I think now you should just stick with what works for you.

Every engine/framework or way of doing things has tons of people constantly complaining about them, nothing is perfect.
[Even Unity still has to this day people complaining about this or that.](https://www.reddit.com/r/Unity3D/comments/n44shs/unity_then_vs_unity_now/)
Maybe those are valid complaints, maybe they aren't. But you know better than anyone about if you should switch to something else or just keep at it.

For my part I just think sticking with what I have is better, unless I find another engine/framework that is significantly better and lets me keep using the same workflows for like 90% of the things I do,
since I want to have to relearn things as little as possible.

## Code

### Local code

I've been very big into doing as much as I can "locally" rather than somewhere else. What I mean is code that defines everything
about some functionality in the same place, rather than split off in multiple places.

In my view this leads to much clearer code, despite looking somewhat less organized. One of my most useful constructs is the timer/trigger one,
and I've expanded it significantly to accomodate for this type of local coding. For instance, from SNKRX:

```lua
self.max_waves = self.level_to_max_waves[self.level]
self.wave = 0
self.start_time = 3
self.t:after(1, function()
  self.t:every(1, function()
    if self.start_time > 1 then alert1:play{volume = 0.5} end
    self.start_time = self.start_time - 1
    self.hfx:use('condition1', 0.25, 200, 10)
  end, 3, function()
    alert1:play{pitch = 1.2, volume = 0.5}
    camera:shake(4, 0.25)
    SpawnEffect{group = self.effects, x = gw/2, y = gh/2 - 48}
    self.t:every(function() return #self.main:get_objects_by_classes(self.enemies) <= 0 end, function()
      self.wave = self.wave + 1
      if self.wave > self.max_waves then return end
      self.hfx:use('condition1', 0.25, 200, 10)
      self.hfx:pull('condition2', 0.0625)
      self.t:after(0.5, function()
        if random:bool(self.level_to_distributed_enemies_chance[self.level]) then
          local n = math.ceil((8 + (self.wave-1)*2)/7)
          for i = 1, n do
            self.t:after((i-1)*2, function()
              self:spawn_distributed_enemies()
            end)
          end
        else
          local spawn_type = random:table{'left', 'middle', 'right'}
          local spawn_points = {left = {x = self.x1 + 32, y = gh/2}, middle = {x = gw/2, y = gh/2}, right = {x = self.x2 - 32, y = gh/2}}
          local p = spawn_points[spawn_type]
          SpawnMarker{group = self.effects, x = p.x, y = p.y}
          self.t:after(0.75, function() self:spawn_n_enemies(p, nil, 8 + (self.wave-1)*2) end)
        end
      end)
    end, self.max_waves+1)
  end)
  self.t:every(function() return #self.main:get_objects_by_classes(self.enemies) <= 0 and self.wave > self.max_waves end, function() self.can_quit = true end)
end)
```

This is almost all of the code needed for handling the enemy spawning behavior in SNKRX, and it's all defined here. I especially like the parts that start with `self.t:every(function()`,
because those are uses of an extremely useful abstraction of the form `trigger:every(condition, action)`, which performs the action every time the condition goes from being false to true.

These allow for extremely local code. They're also especially useful for doing enemy behaviors, for instance:

```lua
elseif self.headbutter then
  self.color = orange[0]:clone()
  self.last_headbutt_time = 0
  self.t:every(function() return math.distance(self.x, self.y, main.current.player.x, main.current.player.y) < 64 and love.timer.getTime() - self.last_headbutt_time > 10 end, function()
    if self.headbutt_charging or self.headbutting then return end
    self.headbutt_charging = true
    self.t:tween(2, self.color, {r = fg[0].r, b = fg[0].b, g = fg[0].g}, math.cubic_in_out, function()
      self.t:tween(0.25, self.color, {r = orange[0].r, b = orange[0].b, g = orange[0].g}, math.linear)
      self.headbutt_charging = false
      headbutt1:play{pitch = random:float(0.95, 1.05), volume = 0.2}
      self.headbutting = true
      self.last_headbutt_time = love.timer.getTime()
      self:set_damping(0)
      self:apply_steering_impulse(300, self:angle_to_object(main.current.player), 0.75)
      self.t:after(0.75, function()
        self.headbutting = false
      end)
    end)
  end)
end
```

This is another example where the main enemy behavior is triggered once a condition is met, and then everything needed for that behavior to happen is also defined locally. Another example:

```lua
self.t:after({2, 4}, function()
  self.shooting = true
  self.t:every({3, 5}, function()
    for i = 1, 3 do
      self.t:after((1 - self.level*0.01)*0.15*(i-1), function()
        shoot1:play{pitch = random:float(0.95, 1.05), volume = 0.1}
        self.hfx:use('hit', 0.25, 200, 10, 0.1)
        local r = self.r
        HitCircle{group = main.current.effects, x = self.x + 0.8*self.shape.w*math.cos(r), y = self.y + 0.8*self.shape.w*math.sin(r), rs = 6}
        EnemyProjectile{group = main.current.main, x = self.x + 1.6*self.shape.w*math.cos(r), y = self.y + 1.6*self.shape.w*math.sin(r), color = fg[0], r = r, v = 150 + 5*self.level + 5*new_game_plus,
          dmg = (new_game_plus*0.1 + 1.5)*self.dmg}
      end)
    end
  end, nil, nil, 'shooter')
end)
```

This one uses normal timers rather than conditional triggers, but the spirit is basically the same. We're nesting these functions that happen after some duration or every time some duration passes
and combining them to build the enemy's behavior.

Most of the more fundamental changes I intend to make to my engine in the future have to do with changing it so that it supports this kind of coding more easily across the board,
as I really like it and it makes me very fast at doing everything.

### Parent-child relationships

Like in my last game, this one also suffered from problems regarding objects referencing each other. There are 2 main ways in which this happens, either
one object fully contains another and this object will be responsible for updating and drawing it, or it just contains a reference to it but it's being updated and drawn by a group (which is a container of objects).

Some objects are a better fit for one thing and others for the other, but the main problem that both of those (and others) share is that they're not very standardized. So in one object I might call the parent
`.parent` but in another set I might call it `.p` for some reason. In some objects the child object kills itself if the parent dies, in others it doesn't.

All of these little details and differences in what is basically the same set of operations contributes to making it a fairly opaque thing.

### State transitions

Transitions between different states also suffer from the same problem that the parent-child operations do.
Essentially they're all the same operation but I haven't standardized them to any great degree, meaning that changing states involves setting some variables to true and others to false,
and creating/destroying objects manually.

This works and it's fine, but like in the previous example, there are lots of different types of transitions that I ended up coding over time and they're all disparate when they should be the same.
This adds a significant amount of cognitive overhead whenever I'm working on that kind of code and it's the kind of thing that slows me down somewhat.

### Node refactor

The solution I have for this is one I've been thinking about for months and I've been putting off working on it because it requires a fairly all-encompassing refactor of the engine,
and as I previously stated I want to avoid these as much as possible. But in this case the gains will probably be so significant that it's worth it.

The idea is very simple: inspired by [Amulet](https://www.amulet.xyz/doc/), everything in the codebase can be conceptually simplified if every entity becomes a `Node`.
A node is an object that has a parent and children. Nodes can be added to other nodes and it will form a tree, or a graph, since nodes should also be able to link back to one another arbitrarily.

Every object in the game is going to be turned into a node, which means that everything will start from a root node and be initialized/updated/drawn from there:

```lua
root = Node()
root:append(Node():tag'player')
```

Here a root node is created and a child tagged with the unique identifier `player` attached to it.
This means that in the root's `children` list, the first node will be this `player` node.

Tags can be used to refer to nodes in a quicker way. So, for instance, we could refer to the child node by saying `root.player`.
Similarly, `root.player.parent` automatically is set to refer back to `root`.

This can also be used to make a node a container. For instance, tagging the node above as `enemies` will create a node that is not functionally different from the player other than its name,
but we can use to act as a container for all enemies, since nodes can contain other nodes. So whenever we want to add an enemy to the game we would go `root.enemies:append`.

This simple setup eliminates the need for different types of container objects, or rather, diminishes it, because now they're all bound
by the same underlying node system. I'm 100% sure about this aspect of the system, I'm light on details for everything else.

However I know some things I don't want. I'm confident that I don't want to use nodes to build objects themselves, like using them as components or something (like Godot does).
And I don't want to use nodes to build draw operations (like [Amulet does](https://www.amulet.xyz/doc/#scenes)).
I simply want them as this base conceptual organizing tool that standardizes these types of things across the entire codebase.

I'm unsure on how exactly I want to augment nodes. I want to maximize my use of local coding, so something like this might be cool:

```lua
root:append(Node()
  :tag'arena'
  :init(function()

  end)
  :update(function(dt)

  end)
  :draw(function()

  end)
)
```

I can make it a convention that all nodes have these 3 functions, `init`, `update` and `draw` and they can be defined for each node like this.
Defining the entity's behavior locally like this is useful, but for entities that are created often it's a waste of both memory and processing power to repeat this like this every time.
So for those cases I still have to support a "normal" way of defining classes, which would be similar to how I do it now, where entities would just inherit from Node.

Now, to further augment nodes, one idea I had was something like this:

```lua
Node(State):tag'arena'
```

The `Node` constructor can receive any number of arguments which are other nodes, and those other nodes can inject their methods and attributes into the original one, thus extending it with any functionality.
The way this is achieved is through the use of mixins, although the details aren't that important from a high level perspective (it's basically a lot of Lua specific hacking).

The result though is that if the `State` node defines that it expects `on_enter` and `on_exit` to be defined, and that those methods will be called when `.active` becomes true or false respectively,
we now have a basic state switching mechanism. We also need additional functions to be defined on the parent node, like `go_to`, which would go from one state to the other and do the work setting `.active`
to true and false as needed, and I'm not entirely sure how to handle that yet.

Maybe if the parent nodes sees that it has nodes that are states as its children then it treats them slightly differently and enables the use of those state specific functions.
This probably means a specific type of node that manages multiple states as its children. Either way, this specific node would also be implemented with the mixin mechanism:

```lua
root:append(Node(StateManager):tag'main')
```

You get the idea. I'm looking forward to trying out this idea and when I release my next game I'll write an update on if it worked or not!

# Design

## Stats

### How stats work

Most stats in the game are a combination of character, class and modifier stat multipliers.

For instance, the Dual Gunner is both a Rogue and a Ranger, which means that his final attack speed is calculated by multiplying the attack speed modifiers for each of those classes,
which are 1.1 and 1.5, and then multiplying that by any additional modifiers, like a Chronomancer's global 20% attack speed buff, which would be 1.2, resulting in a final multiplier of 1.1\*1.5\*1.2 which would be 1.98.

This value would then be used to divide how often the Dual Gunner attacks, which is every 2 seconds, resulting in a final attack rate of ~1 attack per second.

### Multiple characters

Every stat in the game (HP, damage, attack speed, movement speed, AoE damage and size and defense) goes through this process for every character and every enemy.
This is how I also did it for BYTEPATH and that roughly worked out, so I saw no reason to change it.

This game has an additional challenge though, which is that instead of having one character, you have several.
This means that a generally very noticeable 100% damage increase is not that noticeable anymore if it's only happening to 1 out of 8 characters,
since all other characters are also attacking and the increase to that single one isn't really going to be seen or felt.

Both this game and BYTEPATH were inspired somewhat by Path of Exile, which has a similar problem. One of the problems all these games that do stats like this have is that the stat system is very opaque,
and the only feedback you get is if you're passing the DPS/defense checks or not. If you are then you can keep playing, if you aren't then you need to find better gear/passives or try a different build altogether.

This effect is a problem when you're controlling 1 character but it's a seriously bigger problem when you're controlling several. The end result of this is that in SNKRX the build you use ultimately doesn't really matter except for flavor. It's a really brutal "you're either passing the DPS/defense check or not" type of situation and the thing that I was originally going for, which is giving the player lots of build choice, wasn't really achieved.

I noticed this problem fairly early in development but I thought that I could fix it by just adding more characters and passives, and in a way I guess doing that helped,
but it's such a fundamental problem that eventually I had no way to really escape from it without redoing the game from scratch, which I definitely wouldn't do. 

### Artifact

In the future I want to avoid doing opaque stat systems like this. I've been playing a lot of Artifact lately (yes I'm one of the like 50 people that still play it) and I really like the simplicity of its stats.
I guess this simplicity is also true of most card games. In any case, I want to do something more like that rather than these complicated opaque systems.

If you have 10 attack it means you do 10 damage, if you have 10 HP and 2 defense and you take that 10 damage attack, it means you take 8 damage.

If you have 1 attack speed it means you attack at a predefined rate that is global and the same for every unit in the game, like say every 2 seconds,
if you have 10 attack speed it means you attack at a much faster predefined global rate, like say every 0.2 seconds.

Passives that increase your stats should increase them by integer values, so +1 attack speed or +1 damage, and not +10% attack speed or +10% damage.
This will both be simpler to work with and easier to test, while also feeling more impactful and less opaque to players.

## Controls

This is a very simple mistake to make which is that I made the game without thinking about its control scheme.
In general, I want to design games that primarily control really well with either keyboard/gamepad or mouse.

So BYTEPATH controlled pretty well entirely with the keyboard/gamepad, which means that I didn't have to support any mouse interactions in any UI elements.
In the end I think I ended up supporting that for that game, but it 100% wasn't necessary.

In SNKRX the gameplay is keyboard/gamepad oriented, but I did all UI elements to be used with the mouse without thinking about it too much.
I could support 100% keyboard/gamepad gameplay but it's an additional amount of work that I don't feel like doing. So I'll just take this loss for now and remember it for my next games.

## Idea

### A general feeling of stretching the game beyond its limits that feels forced

Overall I feel like the game itself isn't a bad idea but it also isn't a really good one. It's just a very average type of game that does something slightly different:
combining alliance sets with a basic snake gameplay. I don't think I've seen anyone do that before and building your set of classes over a run is kind of fun, so on that front it's good.

But gameplay wise it's a pretty basic game, which isn't bad, but also isn't super good. Fundamentally it's the same game as BYTEPATH where you just move left and right and your
character auto-attacks.

And I don't think anyone complained about that aspect of BYTEPATH. Some people really enjoy just relaxing and having minimal input while tons of things happen automatically,
and this game captures that pretty well, which is why I made it.

At the same time this simplicity can be quite constraining and it can be hard to have good ideas for what you can do with it.
In general I don't have a problem with generating passive/class/item ideas, and this game was no different, but it still always feels like I'm pushing something
way beyond where it can naturally go and it feels forced. 

I don't know. I don't think I've thought about this enough to make my thoughts clear but I'll leave this here for future reference.
Let's call it "a general feeling of stretching the game beyond its limits that feels forced".


# Strategy/Business

## A game every 2 months

### Motivation

Since the start of 2020 I've been trying to make and finish small games consistently.
Projects that take between 1-3 months to make from start to finish and that I actually release on Steam.
For the entirety of 2020 I failed to do that. 

I worked on about maybe ~10 different projects that year and most of them weren't released for anyone to play.
The only one I managed to release in any shape was [a prototype that I made in 3 days at the end of the year](https://a327ex.itch.io/jugglrx-prototype).
I've been inspired by a bunch of people doing this, most prominently [Chilla's Art](https://store.steampowered.com/search/?developer=Chilla%27s%20Art).

The reasons to do this are simple: it seems impossible for me to commit to longer projects in any way. I just don't have the discipline to do it.
Most projects fail in the same way and they're all due to a general lack of direction mixed with poor scoping.
I get way ahead of myself and try making something bigger than I can handle and eventually my motivation drops enough and I just can't work on the project anymore.

### Scoping

So given that this is the problem, it seems like the solution is just starting small and building my game finishing skills and discipline up over time.
However, the reason I failed all this time is also because the kinds of games I want to make naturally tend to be games that are easy to overscope. 

I'm particularly interested in games where you can try lots of builds. Be it with a huge skill tree, lots of items, lots of characters, etc.
Genre doesn't really matter, it can be a roguelite, a base-building tower defense deckbuilder, platformer, whatever, as long as you can play it in lots of different ways.

It's very hard for me to be excited about making small games that don't have this "lots of builds" component.
So over time I've found a way to think about this that has helped me at least deliver this game, and I hope it does many more in the future.

### Small long games

Essentially, you can think of games as either big or small, and either short or long:

Big vs. small refers to how long the project would take to complete and/or how many people. Short vs. long refers to how long the game lasts to the player.
A game that lasts a few minutes or a couple of hours would be short, a game that lasts tens or hundreds of hours would be long.

The space of big games, either short or long is explored by lots of people. The space of small short games is also explored by lots of people, generally indiedevs.
But the space of small long games is largely ignored.

For some reason people assume that projects that last people a long time should also take a long time to make,
but to me it seems like this isn't true. So I've set my sights on exploring this space, largely because it aligns well with what I'm interested in: lots of builds.

### SNKRX

Overall this strategy went well for SNKRX but I fell short of making a long game. I think the game I made before, BYTEPATH, has much more long potential than SNKRX,
so in a way this was a failure. I lost quite a lot of time due to poor decisions that I'll go in the strategy section and
I ended up finishing an initial version of the game 1 month in, and then the next 2 months were spent adding content.  

In the future I should probably take less than a month to finish the initial version of the game. It would be really cool to finish it in 1 week, for instance,
and then have the next 6-7 weeks just for adding content. I think on the whole the strategy of focusing on something small and then expanding on it
with more content over time seems solid, I just need to execute it better and execute on ideas that have more potential to last longer.

## Steam followers

### L. Stotch

A consequence of doing a game every 2 months and releasing each game on Steam is that I can take advantage of the Steam follower feature.

I got this idea from seeing a random dev called [L. Stotch](https://store.steampowered.com/developer/lstotch) on Steam. I have no idea who this is and he doesn't seem to have
a presence anywhere else, still he has about 4k Steam followers and quite a lot of games released since about 2016.

From my own experience with BYTEPATH, I got about 100 followers from it before I mistakenly decided to delete my profile and change my Steam name and lost them all.
But if each game I release gets around that many then it's quite feasible to build a few thousand followers over the years which should help somewhat.

### E-mail

The specific way in which this helps is that everyone who follows you on Steam gets sent an e-mail whenever you release a new game. So essentially it's as if
every game you released automatically had as many wishlists as you have followers by default. This means that L. Stotch, for instance, has about 4k wishlists per game he releases.

This kind of wishlist is probably weaker than a normal wishlist, since people might follow you but not be interested in the next games you make, but it's still a pretty good
and solid amount of consistency that you can add to your results, as e-mails are a fairly strong form of marketing.

### Long term

This is also something that most indie developers are just not paying attention to. I said that I'm inspired by a group of indie devs called [Chilla's Art](https://store.steampowered.com/search/?developer=Chilla%27s%20Art).
These guys are very consistent about their release schedule, what kind of game they're releasing and the overall quality you should expect. Yet they simply don't have a Steam developer page.

I'd guess that most devs aren't interested in focusing on this too much because it's essentially locking yourself to Steam in a fairly unhealthy way.
Most indie devs these days seem more interested in looking for alternative sources of income, which is the correct thing to do, and so tying yourself to Steam even more will naturally be seen as a mistake.

Either way, I have no idea if this is a good thing to do or not, because I've found no articles indiedev business oriented articles talking about how useful Steam followers are or not,
but since I'm going to be releasing lots of games it doesn't hurt to focus on it as a sort of long term goal. 

## Having a plan

### PUBG

In a BR game you're put into very uncomfortable spots and whenever you die and try to figure out what went wrong it can often be the case that you reach the conclusion of "because I had no plan".

In essence, I've found that I generally performed better when I committed to a high level plan before doing things. So, "I'm gonna stay here until the circle comes and then move over there"
or "I'm gonna roam around this area in that direction since my back is covered by the circle" or "I know there are 3 guys in that direction and they have to come through here because of the circle so I'm gonna ambush them".

The reason was that whenever I looked back on what went wrong, because I actually had a plan, I could clearly point out where I went wrong and then improve from there.
Whereas if I had no plan it's very easy to reach for the "oh I just got unlucky!" and other similar excuses.

### Indiedev

The same logic applies to indiedev. Looking back at my failures and wondering why they happened it's easy to reach the conclusion of "because I had no plan".
Most games that failed failed because they had no clear vision or north, I was just doing whatever I felt was cool aimlessly. And when the "cool" part was over I simply jumped to the next thing.

And I simultaneously also had no higher level plan, my goal was just "doing games" because that's what I like doing. 
But that wasn't attached to any real concrete plan.

My mindset recently changed and I actually feel like I have a plan now. And it's simple: make a game every 2 months and increase my number of followers on Steam while doing so.

The short time frame helps with a lot of things, as with each game:
  * I can focus on a specific type of game;
  * I can focus on a specific aspect of my engine that I want to improve;
  * I can focus on a specific visual style that I want try out;
  * I can focus on a specific tech that I want to learn;

Or I can also do all of those things at once. Regardless, each project becomes this massive multipurpose project where on top of just making a game, I'm also building up to something larger
and more consistent over time.

It seems dumb but this change in mindset and having these things as real high level goals really helped push through this project and actually finish it. And I hope that this continues for the next projects.

### Design

Most of the time I wasted while making SNKRX was wasted when I didn't know what to do next.
I would finish a set of tasks and then the next set wasn't immediately clear. I could this X or I could do Y, and they'd generally both be these fairly large tasks that I hadn't broken down yet in any way.

That break in continuity would often take me a few days to recover from, but it happened very consistently. I noticed it eventually because I kept a daily devlog for this project and after a point it was obvious
that that was the issue.

Then I started looking back at my previous projects and sort of realizing that they all had the same problem essentially. Just a general lack of direction and I would always quit
when that lack of direction was at its highest.

So in the future I will simply try to plan each project out more. Spend more time thinking about it and perhaps even visually mocking parts of it up so that I have something solid to work from from the start.

## Demo and wishlist building

As previously stated, having a plan is good because you can clearly figure out what went wrong. Going into this game I had a fairly developed plan for how things would go:
I'd make a playable web demo of the game, release it on itch.io and at the same time also release the game's Steam page. If the game's demo was well received then I'd get a boost in wishlists
which would boost my game's page on Steam and I'd get tons of algorithm wishlists as a result.

### Sound bugs

After about 1 month of development I managed to finish the demo, but upon testing it was clear that there were a few bugs that I couldn't fix. Namely the sounds weren't playing properly.
In my view sounds are really important and add a lot to this game, so while I could release a demo with buggy sounds I'd only do so if that really was the only problem the game had.

### Poor reception

But it was also clear that within a few hours of having a few people playtest the game that it just wasn't something I could release in good conscience. Most problems people pointed out from the demo
were things that I knew were problems and that I knew I was going to fix before the game released, but the game just didn't work without those things being there.

This was a clear case of the game in my head being one thing, and me thinking that even if I implemented half of it people would understand that the other half is missing because it's a demo. But it just didn't work
out this way.

Due to the very fast nature of development on a game like this, the half that was missing was fairly important to making the game work at all and playtesters made it clear to me that essentially what
I had was garbage that didn't really work.

### Changing plans

So I pretty quickly decided to not release a demo at all and just release a Steam page. I spent quite a lot of effort making a trailer for it which in retrospect wasn't entirely necessary.
I made a complete trailer with tons of cuts, the kind you expect from a game release, when a way easier one to make with fewer cuts and more gameplay being showcased would have worked just as well.

[This article](https://www.derek-lieu.com/blog/2021/4/18/the-simplest-trailer-to-make-for-your-steam-page) goes over this a little. The main reason why looking back I would have done an easier trailer was because
the effort was pointless. I released my Steam page, posted it everywhere I could and my game didn't really get any traction anywhere, which I should have predicted and assumed would happen.

With my previous game, BYTEPATH, the same happened, and before release basically no one cared about the game and trying to get people to care was pretty pointless. Only after release did I manage to get traction
with it anywhere, and I suspect that with this game it might be the same. I looked back on my Steamworks stats and BYTEPATH released with about 150 wishlists, and SNKRX has about 200 as of 5 days before release.

### Future plans

So for future games, especially these games that I'm making in 1-3 months, as soon as I have like 1-2 minutes of gameplay that can be recorded and be somewhat coherent (it doesn't even have to be a complete gameplay loop),
I'm going to grab that, record it a little, cut it up into a trailer in a very minimal way, and then make the game's Steam page.
This should probably be done in week 1 or so of development, since I want the page to be up for as long as possible.

At the same time, I shouldn't worry at all about trying to build up my wishlist count once the page is up.
If SNKRX goes like BYTEPATH, which is that it gets a good reception on places like reddit which drives quite a few sales on the first few days, then it's safe to assume that getting good posts on a few subreddits
on release day works better than building wishlists for these smaller games.

I guess I'll know how it goes once SNKRX releases. In case SNKRX doesn't get any good reception at all, then it will sell fairly poorly since 200-300 wishlists is basically nothing. In that case I don't think I have
any plans other than making my next game better (especially visually) so that the chances people upvote it are higher.

## Devlog

One very positive thing about this game's development was that I kept a devlog of it. So after every day or every week I'd write what I did in that time frame and after a while of doing this
it became pretty easy to see what was holding me back and what wasn't.

I already went over these, but mainly it was that whenever I didn't have the next thing to do planned it would take me quite a while to get back to being productive on the project since I'd need to spend
some time thinking about what to do next and for some reason that tended to consume a few days.

Maybe on top of that devlog I should also have some kind of planning document. On the devlog it was often the case that I would write something like "and what I'm gonna do tomorrow is this". Maybe I should try
to develop that spirit of "what I'm gonna do tomorrow" more and have it in a more organized manner in another document.

## Workload 

Overall I'm fairly happy with how much I worked on this project. I definitely didn't overwork myself at all, but I also wasn't super omega lazy.

As I'm writing this, 5 days before the game releases, there are still quite a few things to do but it feels very under control and I don't feel rushed at all. I only feel that my energy to work on this particular
project has been decreasing over time, which is to be expected I think.

With BYTEPATH I had a quite severe "post release depression" period, which I think is something that happens commonly with developers. I feel like with this game I won't really have that at all because I already
know what I need to do next, which is to refactor my engine and then start working on the next game.

## Social media posting

## Release expectations vs. results

## Post-release depression

##

# End

I'd say I'm satisfied that I finally released another game and that I have an immediate plan to do more games in the near future. I hope I can keep myself to this ~2 months schedule.

One of the hard things about releasing games is that it's very hard to get things up to a level you're happy with releasing. You don't want to let go of your standards completely because then
you're just putting pure garbage into the world, but you also don't want the filter to be too strict otherwise you'll never release anything.

Striking a balance that works for you personally can be very difficult, and I think I've finally managed to do it. Let's see if it works!
