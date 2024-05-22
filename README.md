// Pac-Man game in JavaScript using Phaser

// Game configuration
const gameConfig = {
  type: Phaser.CANVAS,
  parent: 'game-container',
  width: 448,
  height: 512,
  scene: {
    preload: preload,
    create: create,
    update: update
  }
};

// Game objects
let pacMan;
let ghosts;
let pellets;
let scoreText;

// Game variables
let score = 0;
let lives = 3;

// Preload assets
function preload() {
  this.load.image('pacman', 'assets/pacman.png');
  this.load.image('ghost', 'assets/ghost.png');
  this.load.image('pellet', 'assets/pellet.png');
  this.load.image('wall', 'assets/wall.png');
}

// Create game objects
function create() {
  // Create Pac-Man
  pacMan = this.add.sprite(224, 256, 'pacman');
  pacMan.setScale(2);
  pacMan.setCollideWorldBounds(true);

  // Create ghosts
  ghosts = [];
  for (let i = 0; i < 4; i++) {
    const ghost = this.add.sprite(224, 256, 'ghost');
    ghost.setScale(2);
    ghost.setCollideWorldBounds(true);
    ghosts.push(ghost);
  }

  // Create pellets
  pellets = [];
  for (let i = 0; i < 240; i++) {
    const pellet = this.add.sprite(Math.random() * 448, Math.random() * 512, 'pellet');
    pellet.setScale(2);
    pellets.push(pellet);
  }

  // Create walls
  for (let i = 0; i < 20; i++) {
    const wall = this.add.sprite(i * 32, 0, 'wall');
    wall.setScale(2);
  }

  // Create score text
  scoreText = this.add.text(10, 10, 'Score: 0', { fontSize: 24, fill: '#ffffff' });
}

// Update game logic
function update(time, delta) {
  // Update Pac-Man movement
  if (this.input.keyboard.isDown(Phaser.Input.Keyboard.LEFT)) {
    pacMan.x -= 4;
  } else if (this.input.keyboard.isDown(Phaser.Input.Keyboard.RIGHT)) {
    pacMan.x += 4;
  } else if (this.input.keyboard.isDown(Phaser.Input.Keyboard.UP)) {
    pacMan.y -= 4;
  } else if (this.input.keyboard.isDown(Phaser.Input.Keyboard.DOWN)) {
    pacMan.y += 4;
  }

  // Update ghost movement
  for (let i = 0; i < ghosts.length; i++) {
    const ghost = ghosts[i];
    ghost.x += Math.random() * 4 - 2;
    ghost.y += Math.random() * 4 - 2;
  }

  // Check collisions
  for (let i = 0; i < pellets.length; i++) {
    const pellet = pellets[i];
    if (pacMan.x + 16 > pellet.x && pacMan.x - 16 < pellet.x && pacMan.y + 16 > pellet.y && pacMan.y - 16 < pellet.y) {
      score++;
      scoreText.text = `Score: ${score}`;
      pellet.destroy();
    }
  }

  for (let i = 0; i < ghosts.length; i++) {
    const ghost = ghosts[i];
    if (pacMan.x + 16 > ghost.x && pacMan.x - 16 < ghost.x && pacMan.y + 16 > ghost.y && pacMan.y - 16 < ghost.y) {
      lives--;
      if (lives === 0) {
        // Game over
      }
    }
  }
}

// Create the game instance
const game = new Phaser.Game(gameConfig);![Screenshot_20240522-075453](https://github.com/Pato1141/Mi-primer-archivo-/assets/169726494/eda939ca-0507-4d0b-998b-a33e3ba9b524)

