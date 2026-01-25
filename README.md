# Apple Collector (Intermediate)

## Introduction @unplugged
Welcome to The LEAGUE's **intermediate Apple Collector** game!  
In this version, you'll build on the beginner game by adding a **countdown timer**, **automatic apple spawning**, and a **game ending condition**. Your goal is to collect as many apples as possible before time runs out. Let's level up!

## Step 1

Start by setting the background color for your game.

From the ``||scene:Scene||`` category, use ``||scene:set background color||`` and choose a color you like.

```blocks
scene.setBackgroundColor(7)
```

## Step 2

Create your player sprite.

From ``||sprites:Sprites||``, use ``||sprites:create a sprite||`` and name it **player**.  
Set the kind to **Player** and choose the `Collector` image from your assets.

```blocks
scene.setBackgroundColor(7)
let player = sprites.create(assets.image`Collector`, SpriteKind.Player)
```

## Step 3

Make the player move using the controller buttons.

From ``||controller:Controller||``, use ``||controller:move sprite with buttons||``.  
Set both **VX** and **VY** to **100**.

```blocks
scene.setBackgroundColor(7)
let player = sprites.create(assets.image`Collector`, SpriteKind.Player)
controller.moveSprite(player, 100, 100)
```

## Step 4

Keep the player inside the screen so they can't run off the edges.

From ``||sprites:Sprites||``, use ``||sprites:set stay in screen||`` and turn it **ON**.

```blocks
scene.setBackgroundColor(7)
let player = sprites.create(assets.image`Collector`, SpriteKind.Player)
controller.moveSprite(player, 100, 100)
player.setStayInScreen(true)
```

## Step 5

Initialize the score.

From ``||info:Info||``, use ``||info:set score to 0||`` so the game starts with zero points.

```blocks
scene.setBackgroundColor(7)
let player = sprites.create(assets.image`Collector`, SpriteKind.Player)
controller.moveSprite(player, 100, 100)
player.setStayInScreen(true)
info.setScore(0)
```

## Step 6

Add a countdown timer to create urgency.

From ``||info:Info||``, use ``||info:start countdown||`` and set it to **30** seconds.

```blocks
scene.setBackgroundColor(7)
let player = sprites.create(assets.image`Collector`, SpriteKind.Player)
controller.moveSprite(player, 100, 100)
player.setStayInScreen(true)
info.setScore(0)
info.startCountdown(30)
```

## Step 7

Make apples spawn automatically during the game.

From ``||game:Game||``, use ``||game:on game update every||`` and set it to **1500 ms**.

```blocks
let apple: Sprite = null
game.onUpdateInterval(1500, function () {

})
```

## Step 8

Create an apple sprite inside the update block.

From ``||sprites:Sprites||``, create a sprite named **apple**, set its kind to **Food**, and use the `Apple` image from your assets.

```blocks
let apple: Sprite = null
game.onUpdateInterval(1500, function () {
    apple = sprites.create(assets.image`Apple`, SpriteKind.Food)
})
```

## Step 9

Make each apple appear at a random position.

Use ``||sprites:set position||`` with ``||math:pick random||``:
- **x** from 10 to 150  
- **y** from 10 to 110  

```blocks
let apple: Sprite = null
game.onUpdateInterval(1500, function () {
    apple = sprites.create(assets.image`Apple`, SpriteKind.Food)
    apple.setPosition(randint(10, 150), randint(10, 110))
})
```

## Step 10

Increase the score when the player collects an apple.

From ``||sprites:on sprite overlaps||`` with **Player** and **Food**:
- Increase the score by 1
- Destroy the apple sprite

```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    otherSprite.destroy()
})
```

## Step 11

End the game when the countdown reaches zero.

From ``||info:on countdown end||``:
- Show a splash message
- Display the final score
- End the game with a **WIN** and **confetti** effect

```blocks
info.onCountdownEnd(function () {
    game.splash("Time's up!", "You collected " + info.score() + " apples!")
    game.over(true, effects.confetti)
})
```

## Conclusion @unplugged

Great job! You built a timed collection game with automatic spawning and a clear win condition.

**Try these challenges:**
- Change the countdown length
- Adjust the apple spawn speed
- Add apples worth different points
- Add obstacles to avoid
- Add sound effects when collecting apples
