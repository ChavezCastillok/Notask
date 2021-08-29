<script>
  import SelectBulmaColors from "./selectBulmaColors.svelte";

  export let notasks;
  export let task;

  let colorSelected = task.color;

  $: task.color = colorSelected;

  function delete_notask(id) {
    notasks = notasks.filter((item) => item.id !== id);
  }
</script>

<section class="message {task.color}">
  <article class="message-header">
    <h5 bind:textContent={task.title} contenteditable="true" title="edit" />
    <button
      class="delete"
      on:click={delete_notask(task.id)}
      title="delete note"
    />
  </article>

  <article class="message-body">
    <p bind:innerHTML={task.text} contenteditable="true" title="edit" />
    <hr />
    <p class="level">
      <SelectBulmaColors bind:colorSelected />
      <span class="help num" title="created date">
        {task.created}
      </span>
    </p>
  </article>
</section>

<style>
  h5 {
    font-weight: bolder;
    width: 100%;
  }
</style>
