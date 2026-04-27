<script>
    let {
        initialCount: count = $bindable(0),
        willIncrement = () => {},
        didIncrement = () => {}
     } = $props()

    let doubled = $derived(count * 2)

    const increment = () => {
        willIncrement(count)
        count++
        didIncrement(count)
    }
</script>

<button onclick={(increment)}>
    clicks:  {count}
</button>

<span>doubled is {doubled}</span>
