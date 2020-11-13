---
layout: post
title:      "Let's Talk About Relationships"
date:       2020-11-13 19:06:37 +0000
permalink:  lets_talk_about_relationships
---


The first obstacle of the rails project (besides deciding on an idea) was establishing and working out your relationships. While they seem like such a small piece of the project code wise, they are foundational element of making your website work. One of the best places to start out is mapping out your relationships. This can be done on paper or on the computer. If you opt to create a digital mock-up of your relationships I highly suggest you use *lucidchart*. Their ads are not only **hilarious** *but*, they also offer may symbotic tools that can help you to easily visualize your project. Below is my final mockup of my tables and my relationships, but let me tell you, it was a LONG road getting here. 

![](https://imgur.com/GoMAmmE)

Now, let's talk about finding your relationships. The basic relationship in my opinion is a belongs_to and has_many relationship. In my project I incorporated two of these:

![](https://imgur.com/Cq5M3Mf)

![](https://imgur.com/3LEAxrt)

Has_many and belongs_to relationships normally make sense in a realworld instance. When you are crafting your relationships you have to think what object needs to know about the other? In my case the DM knows about their stories but their stories don't have to know about the DM. The same goes for the players and their characters. Once you work out your relationship you want to make sure it is added in your table, using foreign keys, and then designate it in your model! When you put the relationships in your models it looks like this:

```
class Player < ApplicationRecord
has_many :characters
end
```

```
class Character < ApplicationRecord
    belongs_to :player
end
```

```
class Dm < ApplicationRecord
    has_many :stories
end
```

```
class Story < ApplicationRecord
    belongs_to :dm
end
```

These were two of my base relationships, once I knew they were working I added my has_many_throughs on top. These are always a little tricker, especially when they result in a many to many relationship. The difficult part of these relationships is sometimes they don't relate to the real world in the way you think they should here is an example of my many to many  (2 connecting has_many_through relationships) :

![](https://imgur.com/aKwNflD)

Let's talk about these relationships:

- A player has many player games
- A playergame belongs to a player
- A player has many games through playergames
- A game has many playergames
- A playergame belongs to a game
- A game has many players through playergames

The two key statements that make it a many to many relationship are:
- A **player** has many **games** through **playergames**
- A **game** has many **players** through **playergames**

Playergames is my connection or *join* table. Without it the connection of games to players would not work. Through these relationships I can call on the games to create my collection_select box in my form. When the player chooses the game they would like to join the form registers their choice and links their playergame to the game that was create by a DM. Again we have to go to the models to solidify the connections that are established in the tables. 

```
class Game < ApplicationRecord
    has_many :playergames
    has_many :players, through: :playergames
    belongs_to :dm
end
```

```
Class Player < ApplicationRecord
    has_many :characters
    has_many :playergames
    has_many :games, through: :playergames
end
```

```
class Playergame < ApplicationRecord
    belongs_to :player
    belongs_to :game
end
```

The relationships are the foundation of your project. I took my time on these I began where I was confident and worked to my many to many, which was initimidating to me. Take your time and break down your relationships, talk to your cohort, and then make sure that you can see where your connections are happening.
