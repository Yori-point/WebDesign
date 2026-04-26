<script>

        context.clearRect(0, 0, canvas.width, canvas.height)
        context.fillRect(0, 0, size, size)
</script>

<h3>Canvas</h3>

<article>
    <canvas width="100" height="100"></canvas>

    <nav>
        <label>
            Size: <input type="range" bind:value={size}>
        </label>

        <label>
            Color: <input type="color" bind:value={color}>
        </label>
    </nav>
</article>

<style>
    article{
        display: flex;
        gap: 1em;
        align-items: end;
    }

    canvas{
        border: solid 1px black;
    }

    nav{
        display: flex;
        gap: 1em;
        flex-direction: column;
    }

    label{
        display: flex;
        gap: 0.5em;
        align-items: center;
    }
</style>