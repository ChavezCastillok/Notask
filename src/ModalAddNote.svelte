<script>
  export let activeModal = false;
  export let notasks, notask;

  const add_notask = () => {
    if (!notask.text.trim()) {
      console.log("text empty");
      notask.text = "";
      return;
    }
    if (notask.title == "") notask.title = "notitle";
    notask.id = Date.now();
    notask.created = new Date(notask.id).toLocaleString("es-ve");
    notask.text = notask.text.replaceAll("\n", "<br />");
    notasks = [notask, ...notasks];
    notask = {
      id: "",
      title: "",
      text: "",
      created: "",
    };
    activeModal = false;
  };

  function closeModal() {
    activeModal = false;
  }
</script>

{#if activeModal}
  <div class="modal is-active">
    <div class="modal-background" on:click={closeModal} />
    <div class="modal-content">
      <article class="section content has-background-white">
        <h3>
          Note Task
          <span class="tag is-info">{notasks.length + 1}</span>
        </h3>
        <form on:submit|preventDefault={add_notask}>
          <div class="control">
            <input
              class="input"
              type="text"
              bind:value={notask.title}
              placeholder="Notask title"
            />
          </div>
          <!-- svelte-ignore a11y-autofocus -->
          <textarea
            class="textarea"
            name="newTask"
            bind:value={notask.text}
            placeholder="Notask description"
            autofocus
          />
          <div class="control has-text-right">
            <input
              class="button is-small is-warning"
              type="reset"
              value="Clear"
            />
            <input
              class="button is-small is-success"
              type="submit"
              value="Add"
            />
          </div>
        </form>
      </article>
    </div>
    <button
      class="modal-close is-large"
      aria-label="close"
      on:click={closeModal}
    />
  </div>
{/if}
