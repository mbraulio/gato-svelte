<script>
  let currentPlayer = "X";

  let squares = Array(9).fill("");

  function handleSquareClick(index) {
    if (!squares[index]) {
      squares[index] = currentPlayer;
      if (checkWinner()) {
        alert(`¡Jugador ${currentPlayer} ha ganado!`);
        resetBoard();
      } else {
        currentPlayer = currentPlayer === "X" ? "O" : "X";
      }
    }
  }

  function checkWinner() {
    // La lógica de verificación del ganador se mantiene igual.
    const winningCombos = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [2, 4, 6],
    ];

    for (const combo of winningCombos) {
      const [a, b, c] = combo;
      if (
        squares[a] &&
        squares[a] === squares[b] &&
        squares[a] === squares[c]
      ) {
        return true;
      }

    }
    return false;
  }

  function resetBoard() {
    squares = Array(9).fill("");
    currentPlayer = "X";
  }
</script>

<div class="board">
  {#each squares as value, index}
    <div class="square" on:click={() => handleSquareClick(index)}>
      {value}
    </div>
  {/each}
</div>

<style>
  .board {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-gap: 5px;
    text-align: center;
  }

  .square {
    width: 100px;
    height: 100px;
    font-size: 36px;
    border: 2px solid #000;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
  }

  .square:hover {
    background-color: #f0f0f0;
  }
</style>
