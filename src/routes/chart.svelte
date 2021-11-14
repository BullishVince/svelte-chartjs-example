<canvas id="myChart" width="3" height="1"></canvas>

<script>
import {onMount, afterUpdate} from 'svelte';

export let input;
export let labels = [1,2];
let chart;

function createChart(chartType, data) {
    const ctx = document.getElementById('myChart').getContext('2d');
    chart = new Chart(ctx, {
        type: 'line',
        data: {
            labels: labels,
            datasets: [{
                label: 'My First Dataset',
                data: input,
                fill: false,
                borderColor: 'rgb(75, 192, 192)',
                tension: 0.1
            }]
        }
    });
}

export function addRandomValue() {
    input.push(Math.random()*100);
    labels.push(labels.length + 1);
    chart.update();
    console.log("add random value...");
}

onMount(createChart);
afterUpdate(() => {
    chart.update();
});

</script>

<button on:click={addRandomValue}>Add random value to chart</button>