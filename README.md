<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Memory Exploration Game</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/phaser/3.60.0/phaser.min.js"></script>
    <style>
        body {
            margin: 0;
            padding: 0;
            background-color: #f0f8ff;
        }
        canvas {
            display: block;
            margin: 0 auto;
        }
    </style>
</head>
<body>
<script>
// Game configuration
const config = {
    type: Phaser.AUTO,
    width: 800,
    height: 600,
    backgroundColor: '#add8e6',
    scene: {
        preload: preload,
        create: create,
        update: update
    }
};

const game = new Phaser.Game(config);

let player;
let cursors;
let memoryItems;
let messageBox;

function preload() {
    // Load assets
    this.load.image('background', 'https://via.placeholder.com/800x600.png');
    this.load.image('player', 'https://via.placeholder.com/40.png?text=P');
    this.load.image('memory', 'https://via.placeholder.com/50.png?text=M');
}

function create() {
    // Add background
    this.add.image(400, 300, 'background');

    // Add player
    player = this.physics.add.sprite(100, 300, 'player');
    player.setCollideWorldBounds(true);

    // Add memories
    memoryItems = this.physics.add.staticGroup();
    memoryItems.create(400, 300, 'memory');

    // Add interaction
    this.physics.add.overlap(player, memoryItems, collectMemory, null, this);

    // Input controls
    cursors = this.input.keyboard.createCursorKeys();

    // Message box
    messageBox = this.add.text(10, 550, '', {
        fontSize: '16px',
        fill: '#000',
        backgroundColor: '#fff',
        padding: { x: 10, y: 5 }
    }).setScrollFactor(0).setVisible(false);
}

function update() {
    player.setVelocity(0);

    if (cursors.left.isDown) {
        player.setVelocityX(-160);
    } else if (cursors.right.isDown) {
        player.setVelocityX(160);
    }

    if (cursors.up.isDown) {
        player.setVelocityY(-160);
    } else if (cursors.down.isDown) {
        player.setVelocityY(160);
    }
}

function collectMemory(player, memory) {
    memory.disableBody(true, true);
    messageBox.setText('You found a memory: Our first photo together!').setVisible(true);

    // Hide the message box after a delay
    this.time.delayedCall(3000, () => {
        messageBox.setVisible(false);
    });
}
</script>
</body>
</html>
