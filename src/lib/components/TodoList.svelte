<script>
    let todos = $state([
        {title: "Assignment 1", done: false},
        {title: "Assignment 2", done: true},
        {title: "Assignment 3", done: false},
    ])
</script>

<h3>Todo List</h3>

<ul>
    {#each todos as todo}
        <li>
            <label>
                <input type="checkbox" bind:checked={todo.done}>
                {todo.title}
            </label>
        </li>
    {/each}
</ul>