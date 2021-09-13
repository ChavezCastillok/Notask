<script>
  import ModalHelpkc from "./ModalHelpkc.svelte";

  let activeModal = false;
  function displayHelpkc() {
    activeModal = true;
  }
  function handleKeydown(event) {
    const key = event.key;
    const alt = event.altKey;
    if (alt && key == "h") displayHelpkc();
  }
</script>

<svelte:window on:keydown|preventDefault={handleKeydown} />

<ModalHelpkc bind:activeModal />
<footer class="footer">
  <div class="columns is-multiline">
    <article class="column is-one-quarter content">
      <h5>Need help?</h5>
      <!-- svelte-ignore a11y-missing-attribute -->
      <p><a on:click={displayHelpkc}>Keyboard commands</a></p>
    </article>
    <article class="column content has-text-centered">
      <p>
        <strong>Notask</strong> is being developed by
        <a href="https://chavezcastillok.github.io" target="_blank"
          >Kevin Chavez</a
        >, with the beauty of
        <a href="https://bulma.io" target="_blank">Bulma-css</a>
        and the power of
        <a href="https://svelte.dev" target="_blank">Svelte-js</a>.
      </p>
      <p>
        The source code is available on
        <a href="https://github.com/ChavezCastillok/Notask" target="_blank">
          Github
        </a>
      </p>
    </article>
  </div>
</footer>
