# Apple Collector

## Introduction @unplugged
Welcome to Apple Collector! In this game, you'll race against time to collect as many apples as you can before the countdown ends. This tutorial introduces new concepts like scoring, timers, and spawning objects. Let's build it!

## Step 1

Let's set up the game environment by choosing a background color.

From the ``||scene:Scene||`` category, use ``||scene:set background color||`` and pick your favorite color.

```blocks
scene.setBackgroundColor(7)
```

## Step 2

Create the player character who will collect the apples.

From ``||sprites:Sprites||``, ``||sprites:create a sprite||`` and name it **player**. Set the kind to **Player** and choose the `Collector` image from your assets.

```blocks
scene.setBackgroundColor(7)
let player = sprites.create(assets.image`Collector`, SpriteKind.Player)
```

## Step 3

Make the player controllable with the buttons.

From ``||controller:Controller||``, use ``||controller:move sprite with buttons||`` and set the speed to **100** for both vx and vy.

```blocks
scene.setBackgroundColor(7)
let player = sprites.create(assets.image`Collector`, SpriteKind.Player)
controller.moveSprite(player, 100, 100)
```

## Step 4

Keep the player inside the screen so they can't run off the edges.

From ``||sprites:Sprites||``, use ``||sprites:set stay in screen||`` to **ON** for your player sprite.

```blocks
scene.setBackgroundColor(7)
let player = sprites.create(assets.image`Collector`, SpriteKind.Player)
controller.moveSprite(player, 100, 100)
player.setStayInScreen(true)
```

## Step 5

Set up the score counter to track collected apples.

From ``||info:Info||``, use ``||info:set score to 0||`` to start the game with zero points.

```blocks
scene.setBackgroundColor(7)
let player = sprites.create(assets.image`Collector`, SpriteKind.Player)
controller.moveSprite(player, 100, 100)
player.setStayInScreen(true)
info.setScore(0)
```

## Step 6

Add a countdown timer to make the game challenging!

From ``||info:Info||``, use ``||info:start countdown||`` and set it to **30** seconds. The timer will appear at the top of the screen.

```blocks
scene.setBackgroundColor(7)
let player = sprites.create(assets.image`Collector`, SpriteKind.Player)
controller.moveSprite(player, 100, 100)
player.setStayInScreen(true)
info.setScore(0)
info.startCountdown(30)
```

## Step 7

Now let's make apples appear automatically throughout the game.

From ``||game:Game||``, use ``||game:on game update every||`` and set it to **1500** ms (1.5 seconds). This will run code repeatedly during the game.

```blocks
let apple: Sprite = null
game.onUpdateInterval(1500, function () {
	
})
```

## Step 8

Inside the game update interval, create an apple sprite.

``||sprites:Create a sprite||`` called **apple** with kind **Food** and use the `Apple` image from your assets.

```blocks
let apple: Sprite = null
game.onUpdateInterval(1500, function () {
    apple = sprites.create(assets.image`Apple`, SpriteKind.Food)
})
```

## Step 9

Make each apple appear at a random position on the screen.

From ``||sprites:Sprites||``, use ``||sprites:set position||`` for the apple. For the x and y coordinates, use ``||math:pick random||`` from the ``||math:Math||`` category:
- x: random from **10** to **150**
- y: random from **10** to **110**

```blocks
let apple: Sprite = null
game.onUpdateInterval(1500, function () {
    apple = sprites.create(assets.image`Apple`, SpriteKind.Food)
    apple.setPosition(randint(10, 150), randint(10, 110))
})
```

## Step 10

Detect when the player collects an apple and add to the score.

From ``||sprites:Sprites||``, use ``||sprites:on sprite overlaps||`` with **Player** and **Food**. When they overlap:
- ``||info:change score by 1||``
- ``||sprites:destroy||`` the food sprite

```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    otherSprite.destroy()
})
```

## Step 11

Finally, let's end the game when time runs out!

From ``||info:Info||``, use ``||info:on countdown end||``. Inside this event:
- Use ``||game:splash||`` to show the message "Time's up!" 
- On the second line, use ``||text:join||`` from ``||text:Text||`` to combine "You collected ", ``||info:score||``, and " apples!"
- End with ``||game:game over||`` set to **WIN** with the **confetti** effect

```blocks
info.onCountdownEnd(function () {
    game.splash("Time's up!", "You collected " + info.score() + " apples!")
    game.over(true, effects.confetti)
})
```

## Conclusion @unplugged

Awesome work! You've created a timed collection game with spawning objects and scoring! 

**Try these challenges:**
- Change the countdown time to make it easier or harder
- Adjust how often apples spawn (the 1500 ms interval)
- Add different types of food worth different points
- Create obstacles to avoid
- Add sound effects when collecting apples

Have fun customizing your game!


> Open this page at [https://ruizosvaldo.github.io/league_apple2/](https://ruizosvaldo.github.io/league_apple2/)

## Use as Extension

This repository can be added as an **extension** in MakeCode.

* open [https://arcade.makecode.com/](https://arcade.makecode.com/)
* click on **New Project**
* click on **Extensions** under the gearwheel menu
* search for **https://github.com/ruizosvaldo/league_apple2** and import

## Edit this project

To edit this repository in MakeCode.

* open [https://arcade.makecode.com/](https://arcade.makecode.com/)
* click on **Import** then click on **Import URL**
* paste **https://github.com/ruizosvaldo/league_apple2** and click import

#### Metadata (used for search, rendering)

* for PXT/arcade
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
