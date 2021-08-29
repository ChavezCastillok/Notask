<script>
  let taskList = localStorage.getItem("taskList")
    ? JSON.parse(localStorage.getItem("taskList"))
    : [];
  let task = "";

  $: localStorage.setItem("taskList", JSON.stringify(taskList));

  function add_task() {
    if (!task.trim()) {
      console.log("text empty");
      task = "";
      return;
    }
    taskList.unshift(task);
    taskList = taskList;
    task = "";
  }

  function delete_task(index) {
    let result = [];
    for (let ftask of taskList.keys()) {
      if (ftask != index) {
        result.push(taskList[ftask]);
      }
    }
    taskList = result;
  }
  function handleKeydown(event) {
    const key = event.key;
    if (key == "Enter" && task != "") add_task();
  }
</script>

<svelte:window on:keydown|stopPropagation={handleKeydown} />

<section class="message is-primary">
  <article class="message-header">
    <h5>Task List</h5>
  </article>
  <article class="message-body">
    <div class="field has-addons">
      <p class="control">
        <!-- svelte-ignore a11y-autofocus -->
        <input
          class="input"
          bind:value={task}
          placeholder="...write and list your task"
          autofocus
        />
      </p>
      <button class="button is-primary" on:click={add_task}>Add</button>
    </div>

    {#each taskList as ftask, index}
      <section class="level is-mobile">
        <p>
          <span class="tag is-primary">{index + 1}</span>
          {#if ftask == ""}
            {delete_task(index)}
          {:else}
            <span bind:textContent={ftask} contenteditable="true" />
          {/if}
        </p>
        <p>
          <button
            class="delete is-small"
            on:click={() => {
              delete_task(index);
            }}
          />
        </p>
      </section>
    {:else}
      <p>↥ Write and list your first task. ↥</p>
    {/each}
  </article>
</section>

<style>
  h5 {
    font-weight: bolder;
  }
</style>
