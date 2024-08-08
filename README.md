# html-css
 html5 e css3

 <a href="https://adriel-vinicius.github.io/html5-css3/supermercado/index.html">Site de supermercado em html e css</a>


</html>

<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>Snake Game</title>
  <link href="style.css" rel="stylesheet" type="text/css" />

  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;

      overflow: hidden;
    }

    #contador {
      font-size: 2em;
      text-align: center;
      color: #ffffff;
      background-color: blue;
      width: 100px;
      border-radius: 10px;
      
      
      position: relative;
      right: -650px;
      bottom: 550px;
    }
  </style>
</head>

<body>
  <main>
  <canvas id="stage" width="600" height="600"></canvas>
  <div id="contador">000</div>
  </main>

  <script type="text/javascript">
    window.onload = function() {
      var stage = document.getElementById('stage');
      var context = stage.getContext("2d"); // Obtendo o contexto do canvas

      document.addEventListener("keydown", keyPush)

      setInterval(game, 1000 / 15); // Chama a função game a cada 1000/15 milissegundos

      const vel = 1;
      var vx = 0 
      var vy = 0
      
      
      //Cabeça da cobra laele
      
      var px = Math.floor(Math.random() * 10)
      var py = Math.floor(Math.random() * 10)
      
      var tp = 20;
      var qp = 30;

      // Objetos de pontos
      var redx =  Math.floor(Math.random() * qp)
      var redy =  Math.floor(Math.random() * qp)
      var whitex = Math.floor(Math.random() * qp)
      var whitey = Math.floor(Math.random() * qp)
      var purplex = Math.floor(Math.random() * qp)
      var purpley = Math.floor(Math.random() * qp)

      var trail = [];
      var tail = 3;



      function game() {
          //tela infinita
        px += vx;
        py += vy;

        if (px < 0) {
          px = qp - 1;
        }

        if (px >= qp) {
          px = 0;
        }

        if (py < 0) {
          py = qp - 1;
        }

        if (py >= qp) {
          py = 0;
        }

        context.fillStyle = "black"; // Definindo a cor de preenchimento
        context.fillRect(0, 0, stage.width, stage.height); // Preenchendo o canvas com a cor preta

        context.fillStyle = "red"; // Definindo a cor de preenchimento
        context.fillRect(redx * tp, redy * tp, tp, tp);

        context.fillStyle = "white"; // Definindo a cor de preenchimento
        context.fillRect(whitex * tp, whitey * tp, tp, tp);

        context.fillStyle = "purple";
        context.fillRect(purplex * tp, purpley * tp, tp, tp)

        context.fillStyle = "green";
        for (var i = 0; i < trail.length; i++) {
          context.fillRect(trail[i].x * tp, trail[i].y * tp, tp-1, tp-1);

          if (trail[i].x == px && trail[i].y == py) {
            vx = 0; 
            vy = 0;     
          }
        }

        trail.push({ x: px, y: py });
        while (trail.length > tail) {
          trail.shift();
        }

        if (redx == px && redy == py) {
          tail++;
          redx = Math.floor(Math.random() * qp); 
          redy = Math.floor(Math.random() * qp); 
          whitex = Math.floor(Math.random() * qp); 
          whitey = Math.floor(Math.random() * qp);
          purplex = Math.floor(Math.random() * qp); 
          purpley = Math.floor(Math.random() * qp);
        }

        if (whitex == px && whitey == py) {
          tail = tail - (tail/2);
          whitex = Math.floor(Math.random() * qp); 
          whitey = Math.floor(Math.random() * qp); 
        }

        if (purplex == px && purpley == py) {
          location.reload()
        }

        //contador
        let contador = document.getElementById("contador")
        contador.innerHTML = parseInt(tail);

        if (tail < 1) {
          redx = Math.floor(Math.random() * qp); 
          redy = Math.floor(Math.random() * qp); 
          whitex = Math.floor(Math.random() * qp); 
          whitey = Math.floor(Math.random() * qp);
          purplex = Math.floor(Math.random() * qp); 
          purpley = Math.floor(Math.random() * qp);
          tail = 3
        }

      


      }
      
      function keyPush(event) {

        switch (event.keyCode) {
          case 37: //left
            vx = -vel;
            vy = 0;
          break;
          case 38: //up
            vx = 0;
            vy = -vel;
          break;
          case 39: //right
            vx = vel;
            vy = 0;
          break;
          case 40: //down
            vx = 0;
            vy = vel;
          break;
          default:

          break;
        }

      }
    }
  </script>

</body>
</html>
