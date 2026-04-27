<script>
    let todos = $state([
        {title: "Assignment 1", done: false},
        {title: "Assignment 2", done: true},
        {title: "Assignment 3", done: false},
    ])

        let todos = $state([
        {title: "Apple", done: false},
        {title: "Bread", done: false},
        {title: "Salmon", done: false},
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

<h3>Groceries</h3>

<ul>
    {#each groceries as grocery}
        <li>
            <label>
                <input type="checkbox" bind:checked={grocery.done}>
                {grocery.title}
            </label>
        </li>
    {/each}
</ul>