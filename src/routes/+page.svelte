<script lang="ts">
  interface Todo {
    text: string;
    completed: boolean;
    createdAt: Date;
  }

  let todos: Todo[] = [
    {
      text: "Learn Svelte",
      completed: false,
      createdAt: new Date()
    },
    {
      text: "Learn SvelteKit",
      completed: false,
      createdAt: new Date()
    },
    {
      text: "Learn TailwindCSS",
      completed: false,
      createdAt: new Date()
    }
  ];

  const formatDate = (date: Date) => {
    return `${date.getMonth()}/${date.getDate()}/${date.getFullYear()}`
  }

  let newTodoText = "";
  const addTodo = (text: string) => {
    if (text === "") return;
    const newTodo: Todo = {
      text,
      completed: false,
      createdAt: new Date()
    };
    todos = [newTodo, ...todos];
    console.log(todos);
    newTodoText = "";
  };

  const deleteTodo = (index: number) => {
    todos = todos.filter((todo, i) => i !== index);
  }

</script>


<div class="h-screen w-screen flex justify-center items-center">
  <div class="w-1/2">
    <h1 class="text-3xl font-bold flex justify-center">Svelte Todo</h1>
    <input
      bind:value={newTodoText}
      type="text"
      placeholder="new todo item"
      class="w-full border-2 border-gray-300 rounded-md p-2 mt-5"
    />
    <button
      on:click={() => addTodo(newTodoText)}
      class="w-full bg-blue-500 text-white p-2 rounded-md mt-2"
    >
      Add Todo
    </button>
    {#each todos as todo, index}
      <div class="flex justify-between items-center mt-2">
        <div class="flex items-center gap-2">
          <input type="checkbox" bind:checked={todo.completed} />
          <p>{todo.text}</p>
          <p>{formatDate(todo.createdAt)}</p>
        </div>
        <button class="bg-red-500 text-white p-2 rounded-md" on:click={() => deleteTodo(index)}>Delete</button>
      </div>
    {/each}

  </div>
</div>