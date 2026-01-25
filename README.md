# Apple Collector (Intermediate)

## Introduction @unplugged
Welcome to **The LEAGUE's Apple Collector game (Intermediate)**!  
In this version of the game, you'll build on what you learned in the beginner tutorial by adding a **countdown timer**, **automatic apple spawning**, and a **game ending condition**. Try to collect as many apples as you can before time runs out!

## Step 1

First, let's set up the game world with a background color.

From the ``||scene:Scene||`` category, use ``||scene:set background color||`` and choose a color you like for your game.

```blocks
scene.setBackgroundColor(7)
```

## Step 2

Now create your player character who will collect the apples.

From ``||sprites:Sprites||``, click and drag ``||sprites:set mySprite to sprite kind player||`` and rename it **myPlayer**.  
Set the kind to **Player** and choose an image from the **Gallery** image section.

```blocks
scene.setBackgroundColor(7)
let myPlayer = sprites.create(assets.image`collector`, SpriteKind.Player)
```

## Step 3

Let's make the player move with the controller buttons!

From ``||controller:Controller||``, use ``||controller:move sprite with buttons||``.  
Press the **+** sign to show both values and set **VX** and **VY** to **100**.

```blocks
scene.setBackgroundColor(7)
let myPlayer = sprites.create(assets.image`collector`, SpriteKind.Player)
controller.moveSprite(myPlayer, 100, 100)
```

## Step 4

Keep the player inside the screen boundaries so they don't disappear off the edges.

From ``||sprites:Sprites||``, use ``||sprites:set stay in screen||`` and turn it **ON** for your player sprite.

```blocks
scene.setBackgroundColor(7)
let myPlayer = sprites.create(assets.image`collector`, SpriteKind.Player)
controller.moveSprite(myPlayer, 100, 100)
myPlayer.setStayInScreen(true)
```

## Step 5

Initialize the score to keep track of how many apples you collect.

From ``||info:Info||``, use ``||info:set score to 0||`` to start the game with zero points.

```blocks
scene.setBackgroundColor(7)
let myPlayer = sprites.create(assets.image`collector`, SpriteKind.Player)
controller.moveSprite(myPlayer, 100, 100)
myPlayer.setStayInScreen(true)
info.setScore(0)
```

## Step 6

Now add a countdown timer to the game.

From ``||info:Info||``, use ``||info:start countdown||`` and set it to **30** seconds.  
This timer will count down while the game is running.

```blocks
scene.setBackgroundColor(7)
let myPlayer = sprites.create(assets.image`collector`, SpriteKind.Player)
controller.moveSprite(myPlayer, 100, 100)
myPlayer.setStayInScreen(true)
info.setScore(0)
info.startCountdown(30)
```

## Step 7

Now let's make apples appear automatically throughout the game.

From ``||game:Game||``, drag out ``||game:on game update every||`` and set it to **2000** ms  
(which means every 2 seconds, a new apple will appear).

```blocks
game.onUpdateInterval(2000, function () {

})
```

## Step 8

Inside the game update interval, create an apple sprite.

Choose ``||sprites:set mySprite to sprite of kind player||`` and:
- Rename it to **apple**
- Change the kind to **Food**
- Use the **apple** image from your assets

```blocks
let apple: Sprite = null
game.onUpdateInterval(2000, function () {
    apple = sprites.create(assets.image`apple`, SpriteKind.Food)
})
```

## Step 9

Make each apple appear at a random position on the screen.

From ``||sprites:Sprites||``, use ``||sprites:set mySprite position to x and y||`` for the apple.  
For both x and y, use ``||math:pick random||`` from ``||math:Math||``:
- x: random from **10** to **150**
- y: random from **10** to **110**

```blocks
let apple: Sprite = null
game.onUpdateInterval(2000, function () {
    apple = sprites.create(assets.image`apple`, SpriteKind.Food)
    apple.setPosition(randint(10, 150), randint(10, 110))
})
```

## Step 10

Make it so collecting apples increases your score.

From ``||sprites:Sprites||``, use  
``||sprites:on sprite of kind player overlaps with otherSprite of kind player||``  
Change the second **Player** to **Food**.

When they overlap:
- ``||info:change score by 1||``
- ``||sprites:destroy||`` **otherSprite**

```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    otherSprite.destroy()
})
```

## Step 11

End the game when the countdown timer reaches zero.

From ``||info:Info||``, use ``||info:on countdown end||``.  
Inside this block:
- Use ``||game:splash||`` to say **"Time's up!"**
- Show how many apples were collected
- End the game with a **WIN** and **confetti** effect

```blocks
info.onCountdownEnd(function () {
    game.splash("Time's up!", "You collected " + info.score() + " apples!")
    game.over(true, effects.confetti)
})
```

## Conclusion @unplugged

Great work! You've upgraded your game with a timer and a win condition.

**What you learned:**
- Using countdown timers
- Ending a game when time runs out
- Showing final results
- Combining score and text messages

**Try these challenges:**
- Change the countdown time
- Make apples spawn faster or slower
- Add different foods worth more points
- Add obstacles to avoid
- Add sound effects when collecting apples

Keep building and keep experimenting!
