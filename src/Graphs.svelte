<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher(); 
    
    export let location;
    export let labels;
    export let values;

    import {afterUpdate} from 'svelte';

    let ctx;
    let chart;

    function creatChart() {
        ctx = document.getElementById('myChart');
        if (chart) {
            chart.destroy();
        }
        chart = new Chart(ctx, {
            // The type of chart we want to create
            type: 'bar',

            // The data for our dataset
            data: {
                labels,
                datasets: [{
                    label: location,
                    backgroundColor: function(context) {
                        var index = context.dataIndex;
                        var value = context.dataset.data[index];
                        return index % 2 ? 'black' : 'white';
                },
                    borderColor: 'black',
                    data: values
                }]
            },

            // Configuration options go here
            options: {}
        });
    }

    afterUpdate(creatChart);
</script>

<canvas id="myChart"></canvas>