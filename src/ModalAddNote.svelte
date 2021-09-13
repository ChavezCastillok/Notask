<script>
  import SelectBulmaColors from "./selectBulmaColors.svelte";

  export let activeModal = false;
  export let notasks, notask;
  let colorSelected;

  let form;
  let noteTitle;
  const add_note = () => {
    if (!notask.text.trim()) {
      console.log("text empty");
      notask.text = "";
      return;
    }

    notask.id = Date.now();
    notask.created = new Date(notask.id).toLocaleString("es-ve");
    notask.text = notask.text.replaceAll("\n", "<br />");
    notask.color = colorSelected;
    notasks = [notask, ...notasks];
    notask = {
      id: "",
      title: "",
      text: "",
      created: "",
      color: "",
    };
    activeModal = false;
  };

  function closeModal() {
    activeModal = false;
  }

  function handleKeydown(event) {
    const key = event.key;
    const alt = event.altKey;
    if (alt && key == "Enter") add_note();
    else if (alt && key == "Backspace") form.reset();
    else if (key == "Escape") closeModal();
  }
</script>

<svelte:window on:keydown|preventDefault={handleKeydown} />

<div class="modal {activeModal ? 'is-active' : ''}">
  <div class="modal-background" on:click={closeModal} />
  <div class="modal-content">
    <article class="section content has-background-white">
      <h3 class="title has-text-white">
        New Note
        <span class="tag {colorSelected}">{notasks.length + 1}</span>
      </h3>
      <form on:submit|preventDefault={add_note} bind:this={form}>
        <label class="control">
          <input
            class="input {colorSelected}"
            type="text"
            bind:this={noteTitle}
            bind:value={notask.title}
            placeholder="Notask title"
          />
        </label>
        <!-- svelte-ignore a11y-autofocus -->

        <textarea
          class="textarea {colorSelected}"
          name="newNote"
          bind:value={notask.text}
          placeholder="Note description"
          autofocus
        />

        <div class="level mt-2">
          <div class="level-left">
            <span class="tag {colorSelected} mr-1">color:</span>
            <SelectBulmaColors bind:colorSelected />
          </div>
          <div class="level-right">
            <div class="control has-text-right">
              <input
                class="button is-small is-warning"
                type="reset"
                value="Clear"
              />
              <input
                class="button is-small is-primary"
                type="submit"
                value="Add"
              />
            </div>
          </div>
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

<style>
  .input,
  .textarea {
    margin: 0.2rem;
  }
</style>
