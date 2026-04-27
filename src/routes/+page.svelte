<script>
    import Canvas from "$lib/components/Canvas.svelte";
    import Counter from "$lib/components/Counter.svelte";
    import TodoList from "$lib/components/TodoList.svelte";

    let count = $state(5)

    $inspect("Count is:", count);
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>

<Counter 
    bind:initialCount={count} 
    willIncrement={(count) => console.log("Count was:", count)}
    didIncrement={(count) => console.log("Count has become:", count)}
    />

{#if count > 10 && count < 20}
    <p>count parent is {count}</p>
{:else if count >30}
    <p>wow! That's a lot of clicks!</p>
{:else}
    <p>count is not in range</p>
{/if}

<Canvas />

<TodoList />

<style>
    h1 {
        color: deepskyblue;
    }
</style>