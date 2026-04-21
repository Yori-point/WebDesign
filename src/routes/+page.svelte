<script>
    import Counter from "$lib/components/Counter.svelte";

    let count = $state(5)

    $inspect(count);
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>

<Counter bind:initialCount={count}/>

<p>count parents is {count}</p>

<style>
    h1 {
        color: deepskyblue;
    }
</style>