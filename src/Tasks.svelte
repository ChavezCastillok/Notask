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

<section class="message is-primary">
  <article class="message-header">
    <h5>Fastasks</h5>
  </article>
  <article class="message-body">
    <div class="field has-addons">
      <p class="control">
        <input
          class="input"
          bind:value={fastask}
          placeholder="...write and list your task"
        />
      </p>
      <button class="button is-primary" on:click={add_fastask}>Add</button>
    </div>

    {#each fastasks as ftask, index}
      <section class="level is-mobile">
        <p>
          <span class="tag is-primary">{index + 1}</span>
          {#if ftask == ""}
            {del_fastask(index)}
          {:else}
            <span bind:textContent={ftask} contenteditable="true" />
          {/if}
        </p>
        <p>
          <button
            class="delete is-small"
            on:click={() => {
              del_fastask(index);
            }}
          />
        </p>
      </section>
    {:else}
      <p>↥ Write and list your first task. ↥</p>
    {/each}
  </article>
</section>
