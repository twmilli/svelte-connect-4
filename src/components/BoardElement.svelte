<script>
  export let element;
  export let handleClick;
  console.log(handleClick);

  const elementToColorMap = {
    0: "white",
    1: "red",
    2: "yellow"
  };

  const colorClass = elementToColorMap[element];
</script>

<style>
  td {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    background-color: pink;
    border: 10px solid #020138;
  }
</style>

<td class={colorClass} on:click={handleClick} />
