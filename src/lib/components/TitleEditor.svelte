<script>
    import { website } from "$lib/state.svelte";
</script>

<h3>Title Editor</h3>

<input type="text" bind:value={website.title}>