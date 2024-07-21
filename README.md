# Bingo-game
A platform where people who love to draw and paint ages ago can have competition  agents someone who love to draw through Bingo game    
<!DOCTYPE html>

<html lang="en">

<head>

  <meta charset="UTF-8">

  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Bingo! - Artistic Edition</title>

  <style>
body {
    font-family: 'Dancing Script', cursive; /* Add a playful font */
      background-image: url("https://www.example.com/subtle-canvas-texture.jpg"); /* Subtle background texture */
      text-align: center;
      margin: 20px;
      color: #333;
    }

    h1 {
      color: #333;
    }

    #bingo-board {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 1px;
      margin-top: 2px;
      border-radius: 1px;
      overflow: hidden;
      background-color: #fff;
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
    }

    .bingo-square {
      height: 90px;
      width: 90px;
      padding: 5px;
      margin: 2px;
      border: 2px solid #ddd;
      text-align: center;
      font-size: 16px;
      cursor: pointer;
      transition: background-color 0.3s;
    }

    .marked {
      background-color: #b7e1cd;
      border-color: #5bb15b;
    }

    .bingo-row, .bingo-column, .bingo-diagonal {
      background-color: #fed330;
      transition: background-color 0.5s;
    }

    #draw-button, #check-button, #clear-button {
      padding: 10px 20px;
      margin-top: 20px;
      cursor: pointer;
      font-size: 16px;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
      transition: background-color 0.3s;
    }

    #draw-button:hover, #check-button:hover, #clear-button:hover {
      background-color: #45a049;
    }

    @media only screen and (max-width: 480px) {
      #bingo-board {
        grid-template-columns: repeat(5, 1fr);
      }

      .bingo-square {
        height: 60px;
        width: 60px;
        padding: 5px;
        font-size: 14px;
      }

      #draw-button, #check-button, #clear-button {
        font-size: 14px;
      }
    }
  
  </style>

</head>

<body>

  <h1>Bingo! - Artistic Edition</h1>

  <div id="bingo-board"></div>

  <button id="draw-button">Draw Theme</button>

  <button id="clear-button">Clear Board</button>

  <button id="check-button">Check for Bingo</button>

  <script>



    function checkForBingo() {

      checkRows();

      checkColumns();

      checkDiagonals();

    }



    function checkRows() {

      for (let i = 0; i < 5; i++) {

        let isBingo = true;

        for (let j = 0; j < 5; j++) {

          const square = document.querySelector(`#bingo-board div:nth-child(${i * 5 + j + 1})`);

          if (!square.classList.contains('marked')) {

            isBingo = false;

            break;

          }

        }

        if (isBingo) {

          highlightBingo('row', i);

          break;

        }

      }

    }



    function checkColumns() {

      for (let i = 0; i < 5; i++) {

        let isBingo = true;

        for (let j = 0; j < 5; j++) {

          const square = document.querySelector(`#bingo-board div:nth-child(${j * 5 + i + 1})`);

          if (!square.classList.contains('marked')) {

            isBingo = false;

            break;

          }

        }

        if (isBingo) {

          highlightBingo('column', i);

          break;

        }

      }

    }



    function checkDiagonals() {

      let isBingoLTR = true;

      for (let i = 0; i < 5; i++) {

        const square = document.querySelector(`#bingo-board div:nth-child(${i * 5 + i + 1})`);

        if (!square.classList.contains('marked')) {

          isBingoLTR = false;

          break;

        }

      }

      if (isBingoLTR) {

        highlightBingo('diagonal', 'ltr');

        return;

      }



      let isBingoRTL = true;

      for (let i = 0; i < 5; i++) {

        const square = document.querySelector(`#bingo-board div:nth-child(${(i + 1) * 5 - i})`);

        if (!square.classList.contains('marked')) {

          isBingoRTL = false;

          break;

        }

      }

      if (isBingoRTL) {

        highlightBingo('diagonal', 'rtl');

      }

    }



    function highlightBingo(type, index) {

      if (type === 'row') {

        for (let j = 0; j < 5; j++) {

          const square = document.querySelector(`#bingo-board div:nth-child(${index * 5 + j + 1})`);

          square.classList.add('bingo-row');

        }

      } else if (type === 'column') {

        for (let j = 0; j < 5; j++) {

          const square = document.querySelector(`#bingo-board div:nth-child(${j * 5 + index + 1})`);

          square.classList.add('bingo-column');

        }

      } else if (type === 'diagonal') {

        if (index === 'ltr') {

          for (let i = 0; i < 5; i++) {

            const square = document.querySelector(`#bingo-board div:nth-child(${i * 5 + i + 1})`);

            square.classList.add('bingo-diagonal');

          }

        } else if (index === 'rtl') {

          for (let i = 0; i < 5; i++) {

            const square = document.querySelector(`#bingo-board div:nth-child(${(i + 1) * 5 - i})`);

            square.classList.add('bingo-diagonal');

          }

        }

      }

      setTimeout(() => {

        alert(`Bingo! You got a ${type}!`);

      }, 500);

    }



    const checkButton = document.getElementById('check-button');

    checkButton.addEventListener('click', checkForBingo);



    const clearButton = document.getElementById('clear-button');

    clearButton.addEventListener('click', () => {

      themes = [...initialThemes];

      shuffleThemes();

      createBingoBoard();

      clearBingoHighlights();

    });



    const bingoBoard = document.getElementById('bingo-board');

    const drawButton = document.getElementById('draw-button');



    let themes = [

      "Impressionist Landscape",

      "Portrait in Monochrome",

      "Abstract Expressionism",

      "Reflections in Water",

      "Urban Decay",

      "Fantasy Realm",

      "Mosaic Art",

      "Metropolis Skyline",

      "Hyperrealistic Eyes",

      "Surreal Dreamscape",

      "Dynamic Sports Moment",

      "Historical Scene",

      "Mechanical Contraptions",

      "Glass Reflections",

      "Ethereal Forest",

      "Vintage Portraits",

      "Architectural Marvels",

      "Smoke and Mirrors",

      "Dynamic Wildlife Action",

      "Celestial Bodies",

      "Futuristic Cityscape",

      "Complex Abstract Geometry",

      "Mastering Light and Shadow",

      "Time Travel Scene",

      "Mythical Creatures"

    ];



    const initialThemes = [...themes];



    function shuffleThemes() {

      themes.sort(() => Math.random() - 0.5);

    }



    function createBingoBoard() {

      bingoBoard.innerHTML = '';

      for (let i = 0; i < themes.length; i++) {

        const square = document.createElement('div');

        square.classList.add('bingo-square');

        square.textContent = themes[i];

        square.addEventListener('click', () => {

          square.classList.toggle('marked');

        });

        bingoBoard.appendChild(square);

      }

    }



    function markSquare(theme) {

      const squares = document.querySelectorAll('.bingo-square');

      for (const square of squares) {

        if (square.textContent == theme) {

          square.classList.add('marked');

        }

      }

    }



    function drawTheme() {

      const randomIndex = Math.floor(Math.random() * themes.length);

      const drawnTheme = themes.splice(randomIndex, 1)[0];

      markSquare(drawnTheme);

    }



    function clearBingoHighlights() {

      const squares = document.querySelectorAll('.bingo-square');

      for (const square of squares) {

        square.classList.remove('marked', 'bingo-row', 'bingo-column', 'bingo-diagonal');

      }

    }



    shuffleThemes();

    createBingoBoard();



    drawButton.addEventListener('click', drawTheme);



  </script>

</body>

</html>
