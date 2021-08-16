<script>
  let notasks = localStorage.getItem("notasks")
    ? JSON.parse(localStorage.getItem("notasks"))
    : [];
  let notask = {
    id: "",
    title: "",
    text: "",
    state: false,
  };

  $: localStorage.setItem("notasks", JSON.stringify(notasks));

  const add_notask = () => {
    if (!notask.text.trim()) {
      console.log("text empty");
      notask.text = "";
      return;
    }
    notask.id = Date.now();
    notasks = [...notasks, notask];
    notask = {
      id: "",
      title: "",
      text: "",
      state: false,
    };
  };

  const delete_notask = (id) => {
    notasks = notasks.filter((item) => item.id !== id);
  };
</script>

<main class="container">
  <section class=" section">
    <div class="columns is-multiline">
      <article class="column is-6-tablet is-4-desktop is-3-fullhd">
        <header class="mb-2">
          <h1 class="title">Notask</h1>
          <h3 class="subtitle">
            ...New <span class="tag is-info">{notasks.length + 1}</span>
          </h3>
        </header>
        <div class="box">
          <form on:submit|preventDefault={add_notask}>
            <div class="control">
              <input
                class="input"
                type="text"
                bind:value={notask.title}
                placeholder="Notask title"
              />
            </div>
            <textarea
              class="textarea"
              name="newTask"
              bind:value={notask.text}
              placeholder="Notask description"
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
        </div>
        <article>
          <h3 class="subtitle">fast task list.</h3>
          <ul>
            <li>
              <strong>#TODO</strong>
            </li>
          </ul>
        </article>
      </article>
      <section class="column columns is-multiline">
        {#each notasks as task, index}
          <article class="column is-full-tablet is-half-desktop is-4-fullhd">
            <section class="box">
              <h3
                class="subtitle has-text-centered"
                bind:textContent={task.title}
                contenteditable="true"
              />
              <p
                class="content {task.state ? 'tachar' : ''}"
                bind:textContent={task.text}
                contenteditable="true"
              />
              <hr />
              <article class="level ">
                <div class="level-left">
                  <span class="tag is-info">{index + 1}</span>
                </div>
                <div class="level-right">
                  <button
                    class="button is-small is-danger m-0"
                    on:click={delete_notask(task.id)}>delete</button
                  >
                </div>
              </article>
            </section>
          </article>
        {:else}
          <article class="section content">
            <h2>Welcome</h2>
            <p>This is a simple app for notes, tasks and or list to do.</p>
            <p>Make your first <strong>Notask</strong> and starting work.</p>
          </article>
        {/each}
      </section>
    </div>
  </section>
</main>

<style>
  .tachar {
    text-decoration: line-through;
  }
</style>
