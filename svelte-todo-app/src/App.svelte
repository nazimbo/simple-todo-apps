<script>
  import { onMount } from "svelte";
  import Todo from "./Todo.svelte";

  let todos = [];
  let newTodoText = "";

  // Load Todos from Local Storage when the component (app) mounts
  onMount(() => {
    const savedTodos = JSON.parse(localStorage.getItem("todos")) || [];
    todos = savedTodos;
  });

  // Add a new todo
  const addTodo = () => {
    if (newTodoText.trim()) {
      todos = [...todos, { id: Date.now(), text: newTodoText, completed: false }];
    }
    newTodoText = "";
    savedTodos();
  };

  // Toggle todo completion status
  const toggleComplete = (id) => {
    todos = todos.map((todo) => {
      return todo.id === id ? { ...todo, completed: !todo.completed } : todo;
    });
    savedTodos();
  };

  // Remove a todo
  const removeTodo = (id) => {
    todos = todos.filter((todo) => todo.id !== id);
    savedTodos();
  };

  // Save Todos to Local Storage when todos change
  const savedTodos = () => {
    localStorage.setItem("todos", JSON.stringify(todos));
  };
</script>

<main>
  <h1>Simple Svelte To-Do App</h1>
  <!-- Form to add a new todo -->
  <form on:submit|preventDefault={addTodo}>
    <input type="text" bind:value={newTodoText} placeholder="What needs to be done?" />
    <button type="submit">Add</button>
  </form>

  <!-- List of todos -->
  <div class="todo-list">
    {#each todos as todo (todo.id)}
      <Todo {todo} {toggleComplete} {removeTodo} />
    {/each}
  </div>
</main>

<style>
  main {
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
    font-family: Arial, sans-serif;
  }

  h1 {
    text-align: center;
    margin-bottom: 30px;
    color: #f44336;
  }

  form {
    display: flex;
    margin-bottom: 20px;
  }

  form input[type="text"] {
    flex-grow: 1;
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 5px 0 0 5px;
  }

  form button[type="submit"] {
    padding: 5px 10px;
    background-color: #f44336;
    color: white;
    border: none;
    border-radius: 0 5px 5px 0;
    cursor: pointer;
  }
</style>
