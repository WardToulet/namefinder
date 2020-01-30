<svelte:head>
	<script src="chart.js" on:load={ chart }></script>
</svelte:head>

<script>
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher(); 
	
	export let location;
	export let labels; export let values; 
	let ctx = document.getElementById('myChart');

	function chart() {
		let chart = new Chart(ctx, {
			// The type of chart we want to create
			type: 'bar',

			// The data for our dataset
			data: {
				labels: labels,
				datasets: [{
					label: location,
					backgroundColor: function(context) {
						let index = context.dataIndex;
						let value = context.dataset.data[index];
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
</script>
<canvas id="myChart"></canvas>
