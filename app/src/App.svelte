<script lang="ts">
  let allTasks = [];
  let inputTask = "";

  function handleCreateButton() {
    const newTask = {
      text: inputTask,
      id: String(new Date().getTime()),
    };

    allTasks = [...allTasks, newTask];
  }

  function handleDeleteButton(event: Event) {
    const target = event.target as HTMLElement;

    const newListOfTasks = allTasks.filter((task) => task.id !== target.id);

    allTasks = newListOfTasks;
  }

  function changeStatusTask(event: Event) {
    const target = event.target as HTMLSpanElement;

    console.log(target.classList);

    target.classList.toggle("selecionado");
  }
</script>

<main>
  <h1>To do list em Svelte</h1>
  <input
    bind:value={inputTask}
    type="text"
    placeholder="Escreva a sua Tarefa aqui..."
  />
  <button on:click={handleCreateButton}>Criar Task</button>

  <ul>
    {#each allTasks as task}
      <li>
        <span on:keypress={changeStatusTask} on:click={changeStatusTask}
          >{task.text}</span
        >
        <button id={task.id} on:click={handleDeleteButton}>Remover Task</button>
      </li>
    {/each}
  </ul>
</main>

<style>
</style>
