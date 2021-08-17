<script>
  export let notasks;
  export let task, index;

  function delete_notask(id) {
    notasks = notasks.filter((item) => item.id !== id);
  }
</script>

<section class="box">
  <article class="content">
    <h5 bind:textContent={task.title} contenteditable="true" />
    <p bind:innerHTML={task.text} contenteditable="true" />
  </article>

  <hr />
  <article class="level is-mobile">
    <div class="level-left">
      <p class="level-item">
        <span class="tag is-info mr-2">{index + 1}</span>
      </p>

      <p class="level-item">
        <small class="help mr-1">Since</small>
        <span class="help is-info num">
          {task.created}
        </span>
      </p>
    </div>
    <div class="level-right">
      <span
        class="tag is-small is-danger m-0"
        on:click={delete_notask(task.id)}
      >
        x
      </span>
    </div>
  </article>
</section>

<style>
  h5 {
    padding: 0.1rem;
    background-color: ghostwhite;
    text-indent: 1rem;
    text-align: center;
  }
</style>
