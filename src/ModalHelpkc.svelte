<script>
  export let activeModal = false;

  const commands = [
    { command: "Enter", description: "to add your fast task" },
    { command: "alt + n", description: "to open create a new note" },
    { command: "alt + Enter", description: "to save the new note" },
    {
      command: "alt + Backspace",
      description: "to clean fields on note creation",
    },
    { command: "Escape", description: "to close create note or this" },
  ];

  function closeModal() {
    activeModal = false;
  }

  function handleKeydown(event) {
    const key = event.key;
    if (key == "Escape") closeModal();
  }
</script>

<svelte:window on:keydown|stopPropagation={handleKeydown} />

{#if activeModal}
  <div class="modal is-active">
    <div class="modal-background" on:click={closeModal} />
    <div class="modal-content">
      <article class="section content has-background-white">
        <h3>Notask</h3>
        <h4>Keyboard commands</h4>
        {#each commands as kc}
          <p>
            <strong class="tag is-primary">{kc.command}</strong>
            {kc.description}
          </p>
        {/each}

        <p class="has-text-centered">
          <span class="help">
            If you need more information,
            <a href="https://chavezcastillok.github.io" target="_blank">
              contact me.
            </a>
          </span>
        </p>
      </article>
    </div>
    <button
      class="modal-close is-large"
      aria-label="close"
      on:click={closeModal}
    />
  </div>
{/if}
