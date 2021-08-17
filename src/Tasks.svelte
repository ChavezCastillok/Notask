<script>
  let fastasks = localStorage.getItem("fastasks")
    ? JSON.parse(localStorage.getItem("fastasks"))
    : [];
  let fastask = "";

  $: localStorage.setItem("fastasks", JSON.stringify(fastasks));

  function add_fastask() {
    if (!fastask.trim()) {
      console.log("text empty");
      fastask = "";
      return;
    }
    fastasks.unshift(fastask);
    fastasks = fastasks;
  }

  function del_fastask(index) {
    let result = [];
    for (let ftask of fastasks.keys()) {
      if (ftask != index) {
        result.push(fastasks[ftask]);
      }
    }
    fastasks = result;
  }
</script>

<section>
  <article class="content box">
    <h5>Fastasks</h5>
    <div class="field has-addons">
      <p class="control">
        <input
          class="input"
          bind:value={fastask}
          placeholder="...write and list your task"
        />
      </p>
      <button class="button is-success" on:click={add_fastask}>Add</button>
    </div>

    {#each fastasks as ftask, index}
      <section class="level is-mobile">
        <p>
          <span class="tag is-info">{index + 1}</span>
          {#if ftask == ""}
            {del_fastask(index)}
          {:else}
            <span bind:textContent={ftask} contenteditable="true" />
          {/if}
        </p>
        <p>
          <span
            class="tag is-danger"
            on:click={() => {
              del_fastask(index);
            }}>x</span
          >
        </p>
      </section>
    {:else}
      <p>↥ Write and list your first task. ↥</p>
    {/each}
  </article>
</section>

<style>
  h5 {
    padding: 0.1rem;
    background-color: ghostwhite;
    text-align: center;
  }
</style>
