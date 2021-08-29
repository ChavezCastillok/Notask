<script>
  let colors = [
    { color: "turquoise", bulmaCode: "is-primary" },
    { color: "cyan", bulmaCode: "is-info" },
    { color: "blue", bulmaCode: "is-link" },
    { color: "yellow", bulmaCode: "is-warning" },
    { color: "red", bulmaCode: "is-danger" },
    { color: "black", bulmaCode: "is-dark" },
    { color: "green", bulmaCode: "is-success" },
  ];
  export let colorSelected = colors[0].bulmaCode;
</script>

<div class="select {colorSelected} is-small ">
  <select bind:value={colorSelected} name="colors">
    {#each colors as color}
      <option value={color.bulmaCode}>{color.color}</option>
    {/each}
  </select>
</div>
