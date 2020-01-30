<svelte:head>
	<script src="chart.js" on:load={ createChart }></script>
</svelte:head>
<script>
	export let nameList = null;

	let ctx;
	let chart = null;

	$: {
		let top = nameList !== null ? nameList.sort((p1, p2) => p1.count > p2.count).slice(0, 5) : [];
		let topNames = top.map(p => p.name);
		let topCount = top.map(p => p.count);

		ctx = document.getElementById('myChart');
		if(chart != null) {
			chart.data = {
				labels: topNames,
				datasets: [{
					backgroundColor: 'black', 
					borderColor: 'black',
					data: topCount 
				}]
			};

			chart.update();
		}
	}

	function createChart() { 
		chart = new Chart(ctx, {
			type: 'horizontalBar',
			options: {}
		});
		console.log(chart);
	}
</script>
<canvas id="myChart"></canvas>
