<script>
    import Chart from './chart.svelte';
    let chartComponent;

    let settings = {
        input: [1,5]
    };
</script>

<h1>Input values below</h1>
<input type="number" bind:value={settings.input}>
<button class="inline" on:click={settings.input.push(2)}>Add value</button>
<Chart bind:this={chartComponent} {...settings}/>