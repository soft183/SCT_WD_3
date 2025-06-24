<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Tic-Tac-Toe Game</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background: #f0f2f5;
      padding: 40px;
    }
    h1 {
      color: #333;
    }
    .board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-gap: 10px;
      justify-content: center;
      margin: 20px auto;
    }
    .cell {
      width: 100px;
      height: 100px;
      background: #fff;
      border: 2px solid #333;
      font-size: 36px;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      transition: 0.3s;
    }
    .cell:hover {
      background: #e2f1ff;
    }
    #message {
      font-size: 20px;
      margin-top: 20px;
      color: #555;
    }
    #reset {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 16px;
      background: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    #reset:hover {
      background: #0056b3;
    }
  </style>
</head>
<body>

  <h1>🎮 Tic-Tac-Toe</h1>

  <div class="board" id="board"></div>

  <div id="message">Player X's turn</div>
  <button id="reset">Reset Game</button>

  <script>
    const board = document.getElementById("board");
    const message = document.getElementById("message");
    const resetButton = document.getElementById("reset");

    let currentPlayer = "X";
    let gameActive = true;
    let gameState = ["", "", "", "", "", "", "", "", ""];

    const winningCombos = [
      [0,1,2], [3,4,5], [6,7,8],
      [0,3,6], [1,4,7], [2,5,8],
      [0,4,8], [2,4,6]
    ];

    function checkWinner() {
      for (let combo of winningCombos) {
        const [a, b, c] = combo;
        if (gameState[a] && gameState[a] === gameState[b] && gameState[a] === gameState[c]) {
          gameActive = false;
          message.textContent = `🎉 Player ${gameState[a]} wins!`;
          return;
        }
      }

      if (!gameState.includes("")) {
        gameActive = false;
        message.textContent = "It's a draw!";
      }
    }

    function handleClick(index) {
      if (!gameActive || gameState[index] !== "") return;

      gameState[index] = currentPlayer;
      cells[index].textContent = currentPlayer;
      checkWinner();

      if (gameActive) {
        currentPlayer = currentPlayer === "X" ? "O" : "X";
        message.textContent = `Player ${currentPlayer}'s turn`;
      }
    }

    function renderBoard() {
      board.innerHTML = "";
      for (let i = 0; i < 9; i++) {
        const cell = document.createElement("div");
        cell.classList.add("cell");
        cell.addEventListener("click", () => handleClick(i));
        board.appendChild(cell);
      }
      cells = document.querySelectorAll(".cell");
    }

    resetButton.addEventListener("click", () => {
      currentPlayer = "X";
      gameActive = true;
      gameState = ["", "", "", "", "", "", "", "", ""];
      message.textContent = `Player ${currentPlayer}'s turn`;
      renderBoard();
    });

    // Initial load
    renderBoard();
  </script>

</body>
</html>
