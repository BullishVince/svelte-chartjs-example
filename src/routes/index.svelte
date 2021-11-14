<script>
    import Chart from './chart.svelte';
    let chartComponent;

    let inputValue;
</script>

<h1>Line chart</h1>
<input type="number" bind:value={inputValue}>
<button class="inline" on:click={chartComponent.addValue(inputValue ?? 0)}>Add value</button>
<Chart bind:this={chartComponent}/>