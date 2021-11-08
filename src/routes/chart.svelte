<canvas id="myChart" width="3" height="1"></canvas>

<script>
import {onMount, afterUpdate} from 'svelte';

export let input;
let chart;

function createChart(chartType, data) {
    const ctx = document.getElementById('myChart').getContext('2d');
    chart = new Chart(ctx, {
        type: 'line',
        data: {
            labels: [1,2,3,4,5,6,7],
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

export function addValue(value) {
    console.log(`update chart with value ${value}`);
    chart.update();
}

onMount(createChart);
afterUpdate(() => {
    chart.update();
});

</script>