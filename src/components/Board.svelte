<script>
  import BoardElement from "./BoardElement.svelte";
  export let width;
  export let height;

  let board = [];
  let currentTurn = 1;
  for (var row = 0; row < height; row++) {
    board.push([]);
    for (var col = 0; col < width; col++) {
      board[row].push(0);
    }
  }

  const handleClick = colIndex => {
    console.log("HELLO");
    for (var row = height - 1; row >= 0; row--) {
      if (board[row][colIndex] == 0) {
        board[row][colIndex] = currentTurn;
      }
    }
    currentTurn += 1;
    if (currentTurn > 2) {
      currentTurn = 1;
    }
    console.log(board);
  };

  $: console.log(board);
</script>

<style>

</style>

<table>
  {#each board as row, rowIndex}
    <tr>
      {#each row as element, colIndex}
        <BoardElement {element} handleClick={() => handleClick(colIndex)} />
      {/each}
    </tr>
  {/each}
</table>
