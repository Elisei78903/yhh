// Create canvas element for game
const canvas = document.createElement('canvas');
canvas.width = 800;
canvas.height = 500;
document.body.appendChild(canvas);

// Get 2D context of canvas
const ctx = canvas.getContext('2d');

// Define player properties
const player = {
  x: canvas.width / 2 - 20,
  y: canvas.height / 2 - 20,
  width: 40,
  height: 40,
  speed: 5,
  score: 0
};

// Define ball properties
const ball = {
  x: canvas.width / 2 - 10,
  y: canvas.height / 2 - 10,
  size: 20,
  speed: 4,
  dx: 4,
  dy: -4
};

// Define goal properties
const goal = {
  x: 0,
  y: canvas.height / 2 - 50,
  width: 40,
  height: 100
};

// Draw players, ball and goals on canvas
function draw() {
  // Clear canvas
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // Draw players
  ctx.fillStyle = 'red';
  ctx.fillRect(player.x, player.y, player.width, player.height);

  // Draw ball
  ctx.fillStyle = 'white';
  ctx.fillRect(ball.x, ball.y, ball.size, ball.size);

  // Draw goals
  ctx.fillStyle = 'blue';
  ctx.fillRect(goal.x, goal.y, goal.width, goal.height);
  ctx.fillStyle = 'red';
  ctx.fillRect(canvas.width - goal.width, goal.y, goal.width, goal.height);
}

// Move player and ball
function update() {
  // Move player
  if (keys.ArrowUp && player.y > 0) {
    player.y -= player.speed;
  }
  if (keys.ArrowDown && player.y < canvas.height - player.height) {
    player.y += player.speed;
  }
  if (keys.ArrowLeft && player.x > 0) {
    player.x -= player.speed;
  }
  if (keys.ArrowRight && player.x < canvas.width - player.width) {
    player.x += player.speed;
  }

  // Move ball
  ball.x += ball.dx;
  ball.y += ball.dy;

  // Check for collision with player
  if (
    ball.x - ball.size / 2 < player.x + player.width &&
    ball.x + ball.size / 2 > player.x &&
    ball.y - ball.size / 2 < player.y + player.height &&
    ball.y + ball.size / 2 > player.y
  ) {
    ball.dx *= -1.1;
    ball.dy *=
