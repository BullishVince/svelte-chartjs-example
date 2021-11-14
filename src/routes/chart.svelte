<canvas id="myChart" width="3" height="1"></canvas>

<script>
import {onMount, afterUpdate} from 'svelte';

export let input = [];
let latestValue;
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
                borderColor: 'rgb(0, 0, 255)'
            }]
        },
        options: {
            plugins: {
                zoom: {
                    limits: {
                        x: {min: -100, max: 100, minRange: 1},
                        y: {min: -100, max: 100, minRange: 1}
                    },
                    pan: {
                        enabled: true,
                        mode: 'y',
                    },
                    zoom: {
                        wheel: {
                        enabled: true,
                        },
                        pinch: {
                        enabled: true
                        },
                        mode: 'xy',
                    onZoomComplete({chart}) {
                        // This update is needed to display up to date zoom level in the title.
                        // Without this, previous zoom level is displayed.
                        // The reason is: title uses the same beforeUpdate hook, and is evaluated before zoom.
                        chart.update('none');
                        }
                    }
                },
            }
        },
    });
}

export function addRandomValue() {
    input.push(Math.random()*100);
    labels.push(labels.length + 1);
    chart.update();
}

export function addValue(value) {
    input.push(value);
    labels.push(labels.length + 1);
    latestValue = value;
}

onMount(createChart);
afterUpdate(() => {
    chart.update();
});

</script>

<button on:click={addRandomValue}>Add random value to chart</button>

<button class="inline" on:click={() => {
    chart.resetZoom();
}}>Reset chart</button>