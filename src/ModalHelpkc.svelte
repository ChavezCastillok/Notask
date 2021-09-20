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
    {
      command: "Escape",
      description: "to close create note or this modal window",
    },
    {
      command: "alt + h",
      description: "to open this help modal window",
    },
  ];

  function handleKeydown(event) {
    const key = event.key;
    if (key == "Escape") activeModal = false;
  }

  function closeModal() {
    activeModal = false;
  }
</script>

<svelte:window on:keydown={handleKeydown} />

<div class="modal {activeModal ? 'is-active' : ''} ">
  <div class="modal-background" on:click={closeModal} />
  <div class="modal-content">
    <article class="section content has-background-white">
      <h3>Notask</h3>
      <h4>Keyboard commands</h4>
      <ul>
        {#each commands as kc}
          <li class="level">
            {kc.description}
            <strong class="tag is-primary">{kc.command}</strong>
          </li>
        {/each}
      </ul>

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
