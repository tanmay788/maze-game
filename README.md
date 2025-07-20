
<!DOCTYPE html>
<html>
<head>
  <title>Car Racing Game</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
    }

    #gameArea {
      width: 400px;
      height: 600px;
      background: #333;
      position: relative;
      margin: 0 auto;
      border: 4px solid #fff;
    }

    .car {
      width: 50px;
      height: 100px;
      position: absolute;
      bottom: 10px;
      background: red;
    }

    .enemy {
      width: 50px;
      height: 100px;
      background: yellow;
      position: absolute;
      top: -120px;
    }
  </style>
</head>
<body>

<div id="gameArea">
  <div class="car" id="playerCar"></div>
</div>

<script>
  const gameArea = document.getElementById('gameArea');
  const playerCar = document.getElementById('playerCar');

  let carLeft = 175;
  playerCar.style.left = carLeft + 'px';

  document.addEventListener('keydown', moveCar);

  function moveCar(e) {
    if (e.key === "ArrowLeft" && carLeft > 0) {
      carLeft -= 10;
    } else if (e.key === "ArrowRight" && carLeft < 350) {
      carLeft += 10;
    }
    playerCar.style.left = carLeft + 'px';
  }

  function createEnemy() {
    const enemy = document.createElement('div');
    enemy.classList.add('enemy');
    enemy.style.left = Math.floor(Math.random() * 350) + 'px';
    gameArea.appendChild(enemy);

    let topPos = -100;

    const interval = setInterval(() => {
      topPos += 5;
      enemy.style.top = topPos + 'px';

      // Collision Detection
      if (topPos > 500 && Math.abs(carLeft - parseInt(enemy.style.left)) < 50) {
        alert('💥 Game Over!');
        location.reload();
        clearInterval(interval);
      }

      if (topPos > 600) {
        enemy.remove();
        clearInterval(interval);
      }
    }, 30);
  }

  setInterval(createEnemy, 1500);
</script>

</body>
</html>
