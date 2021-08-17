<script>
  import Tasks from "./Tasks.svelte";
  import ModalAddNote from "./ModalAddNote.svelte";
  import Note from "./Note.svelte";

  export let title;

  export let notasks = localStorage.getItem("notasks")
    ? JSON.parse(localStorage.getItem("notasks"))
    : [];
  export let notask = {
    id: "",
    title: "",
    text: "",
    created: "",
    color: "",
  };
  let btn_newNote;
  let modalNewNotask = false;
  $: localStorage.setItem("notasks", JSON.stringify(notasks));

  function add_notask() {
    modalNewNotask = true;
  }
</script>

<main class="container is-fullhd">
  <header class="has-text-centered mb-2">
    <h1 class="title has-text-primary">
      {title}
    </h1>
    <h2 class="subtitle has-text-primary">Notes and task list</h2>
  </header>
  <section class="section">
    <div class="columns is-multiline">
      <article class="column is-6-tablet is-4-desktop">
        <Tasks />
      </article>
      {#each notasks as task}
        <article class="column is-6-tablet is-4-desktop">
          <Note bind:notasks bind:task />
        </article>
      {:else}
        <article class="section content">
          <h2>Welcome</h2>
          <p>This is a simple app for notes, tasks and or list to do.</p>
          <p>Make your first <strong>Notask</strong> and starting work.</p>
        </article>
      {/each}
    </div>
    <button
      id="btn_newNote"
      class="button is-primary is-rounded"
      bind:this={btn_newNote}
      on:click={add_notask}
      on:mouseout={() => {
        btn_newNote.innerText = "+";
      }}
      on:mouseover={() => {
        btn_newNote.innerText = "New Note";
      }}
    >
      +
    </button>
    <ModalAddNote bind:activeModal={modalNewNotask} bind:notasks bind:notask />
  </section>

  <footer class="footer">
    <article class="content has-text-centered">
      <p>
        <strong>Notask</strong> is being developed by
        <a href="https://chavezcastillok.github.io">Kevin Chavez</a>, with the
        beauty of <a href="https://bulma.io">Bulma-css</a> and the power of
        <a href="https://svelte.dev">Svelte-js</a>.
      </p>
      <p>
        The source code is available on <a
          href="https://chavezcastillok.github.io">Github</a
        >
      </p>
    </article>
  </footer>
</main>

<style>
  :global(body) {
    font-family: "Comfortaa";
  }
  :global(.title, .subtitle) {
    font-family: "Fredoka One";
    font-weight: 100;
  }
  :global(.num) {
    font-family: "Linux Biolinum G", "Linux Biolinum";
  }
  #btn_newNote {
    position: fixed;
    bottom: 3%;
    right: 3%;
  }
</style>
