<script>
  export let todo;
  export let toggleComplete;
  export let removeTodo;

  const handleComplete = () => {
    toggleComplete(todo.id);
  };

  const handleRemove = () => {
    removeTodo(todo.id);
  };
</script>

<div class="todo">
  <input type="checkbox" checked={todo.completed} on:change={handleComplete} />
  <span class:completed={todo.completed}>{todo.text}</span>
  <button on:click={handleRemove}>Delete</button>
</div>

<style>
  .todo {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px 20px;
    border-bottom: 1px solid #e0e0e0;
  }

  .todo input[type="checkbox"] {
    margin-right: 10px;
    appearance: none;
    -webkit-appearance: none;
    width: 20px;
    height: 20px;
    border: 1px solid #c0c0c0;
    border-radius: 50%;
    background-color: #fff;
    transition: background-color 0.3s ease;
    cursor: pointer;
  }

  .todo input[type="checkbox"]:checked {
    background-color: #4caf50;
    border-color: #4caf50;
  }

  .todo span {
    flex-grow: 1;
    font-size: 16px;
    line-height: 1.4;
    color: #333;
    transition:
      color 0.3s ease,
      text-decoration 0.3s ease;
  }

  .todo span.completed {
    color: #8c8c8c;
    text-decoration: line-through;
  }

  .todo button {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 36px;
    height: 36px;
    background-color: #f44336;
    border: none;
    border-radius: 50%;
    color: #fff;
    font-size: 16px;
    font-weight: bold;
    transition: background-color 0.3s ease;
    cursor: pointer;
  }

  .todo button:hover {
    background-color: #e53935;
  }
</style>
