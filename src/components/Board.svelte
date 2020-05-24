<script>
  import BoardElement from "./BoardElement.svelte";
  export let width;
  export let height;
  let won = false;

  let board = [];
  let currentTurn = 1;
  for (var row = 0; row < height; row++) {
    board.push([]);
    for (var col = 0; col < width; col++) {
      board[row].push(0);
    }
  }

  const handleClick = colIndex => {
    if (won) {
      return;
    }
    for (var row = height - 1; row >= 0; row--) {
      if (board[row][colIndex] == 0) {
        board[row][colIndex] = currentTurn;
        break;
      }
    }
    if (checkWinForPlayer(currentTurn)) {
      won = true;
      return;
    }
    currentTurn += 1;
    if (currentTurn > 2) {
      currentTurn = 1;
    }
  };

  const checkWinForPlayer = player => {
    // horizontalCheck
    for (let row = 0; row < height; row++) {
      for (let col = 0; col < width - 3; col++) {
        if (
          board[row][col] == player &&
          board[row][col + 1] == player &&
          board[row][col + 2] == player &&
          board[row][col + 3] == player
        ) {
          return true;
        }
      }
    }

    // verticalCheck
    for (let row = 0; row < height - 3; row++) {
      for (let col = 0; col < width; col++) {
        if (
          board[row][col] == player &&
          board[row + 1][col] == player &&
          board[row + 2][col] == player &&
          board[row + 3][col] == player
        ) {
          return true;
        }
      }
    }

    // ascendingDiagonalCheck
    for (let col = 0; col < width - 3; col++) {
      for (let row = 3; row < height; row++) {
        if (
          board[row][col] == player &&
          board[row - 1][col + 1] == player &&
          board[row - 2][col + 2] == player &&
          board[row - 3][col + 3] == player
        )
          return true;
      }
    }
    // descendingDiagonalCheck
    for (let col = 3; col < width; col++) {
      for (let row = 3; row < height; row++) {
        if (
          board[row][col] == player &&
          board[row - 1][col - 1] == player &&
          board[row - 2][col - 2] == player &&
          board[row - 3][col - 3] == player
        )
          return true;
      }
    }

    return false;
  };
  $: console.log(board);
</script>

<style>

</style>

<div>
  {#if won}
    <h2>Player {currentTurn} Wins! 🎉</h2>
  {/if}
  <table>
    {#each board as row, rowIndex}
      <tr>
        {#each row as element, colIndex}
          <BoardElement {element} handleClick={() => handleClick(colIndex)} />
        {/each}
      </tr>
    {/each}
  </table>
</div>
