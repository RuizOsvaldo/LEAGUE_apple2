scene.setBackgroundColor(7)
let player = sprites.create(assets.image`Collector`, SpriteKind.Player)
controller.moveSprite(player, 100, 100)
player.setStayInScreen(true)
info.setScore(0)
info.startCountdown(30)

let apple: Sprite = null
game.onUpdateInterval(1500, function () {
    apple = sprites.create(assets.image`Apple`, SpriteKind.Food)
    apple.setPosition(randint(10, 150), randint(10, 110))
})

sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    info.changeScoreBy(1)
    otherSprite.destroy()
})

info.onCountdownEnd(function () {
    game.splash("Time's up!", "You collected " + info.score() + " apples!")
    game.over(true, effects.confetti)
})