<script>
    let count = $state(2)
    let doubled = count * 2
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://svelte.dev/docs/kit">svelte.dev/docs/kit</a> to read the documentation</p>

<button onclick={() => count++ }>
    clicks: {count}
</button>

<span>double is {doubled}</span>

<style>
    h1 {
        color: deepskyblue;
    }
</style>