<script>
    let count = $state(0)
    let doubled = $derived (count * 2)
</script>

<button onclick={() => count++ }>
    clicks: {count}
</button>

<span>double is {doubled}</span>
