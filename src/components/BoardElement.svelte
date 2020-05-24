<script>
  export let element;
  export let handleClick;

  const elementToColorMap = {
    0: "white",
    1: "red",
    2: "yellow"
  };

  $: colorClass = elementToColorMap[element];
</script>

<style>
  .white {
    background-color: #f8f8ff;
  }

  .red {
    background-color: #fe1422;
  }

  .yellow {
    background-color: #feed04;
  }
  td {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    border: 10px solid #020138;
  }
</style>

<td class={colorClass} on:click={handleClick} />
