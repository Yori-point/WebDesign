<script>
    let todos = $state([
        {title: "Assignment 1", done: false},
        {title: "Assignment 2", done: true},
        {title: "Assignment 3", done: false},
    ])

        let groceries = $state([
        {title: "Apple", done: false},
        {title: "Bread", done: false},
        {title: "Salmon", done: false},
    ])
</script>

{#snippet todoItem(todo)}
    <li>
      <label>
          <input type="checkbox" bind:checked={todo.done}>
         {todo.title}
         </label>
  </li>
{/snippet}

<h3>Todo List</h3>

<ul>
    {#each todos as todo}
        {@render todoItem(todo)}
    {/each}
</ul>

<h3>Groceries</h3>

<ul>
    {#each groceries as grocery}
        {@render todoItem(grocery)}
    {/each} 
</ul>