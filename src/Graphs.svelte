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

		if(chart !== null) {
			console.log(chart);

			if(chart.data.datasets[0] != null) {
				for(let i = 0; i < chart.data.datasets[0].data.length; i++) {
					console.log('test');
					console.log(i);
					chart.data.datasets[0].data[i] = topCount[i];
				}
			} else {
				chart.data.datasets.push({
					data: topCount
				});
			}

			chart.data.labels = topNames;
			chart.update();
		}
	}

	function createChart() { 
		ctx = document.getElementById('myChart');
		chart = new Chart(ctx, {
			type: 'horizontalBar',
			data: {
				options: {
					legend: {
						display: false
					}
				},
				datasets: []
			}
		});
		console.log(chart);
	}
</script>
<canvas id="myChart"></canvas>
