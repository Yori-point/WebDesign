<script>
    let props = $props()

    let count = $state(props.initialCount)
    let doubled = $derived (count * 2)
</script>

<button onclick={() => count++ }>
    clicks: {count}
</button>

<span>double is {doubled}</span>
