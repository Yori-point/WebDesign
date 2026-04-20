<script>
    let { initialCount } = $props()

    let doubled = $derived (initialCount * 2)
</script>

<button onclick={() => initialCount++ }>
    clicks: {initialCount}
</button>

<span>doubled is {doubled}</span>
