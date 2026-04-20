<script>
    let { initialCount: count } = $props()

    let doubled = $derived (count * 2)
</script>

<button onclick={() => count++ }>
    clicks: {count}
</button>

<span>doubled is {doubled}</span>
