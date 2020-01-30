<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher(); 
    
    export let location;
    export let labels;
    export let values;

    var ctx = document.getElementById('myChart');

    let chart = new Chart(ctx, {
        // The type of chart we want to create
        type: 'bar',

        // The data for our dataset
        data: {
            labels: labels,
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
</script>

<canvas id="myChart"></canvas>