<script>
	import Map from './Map.svelte';
	import YearSlider from './YearSlider.svelte';

	let namesByYearByPlace = getJSON('byYearByPlace');
	let placeNameById = getJSON('gemeenten');

	async function getJSON(name) {
		let res = await fetch(`./data/${name}.json`);
		let obj = await res.json();

		console.log(obj);

		if(!res.ok)
			return new Error(obj);

		return obj;
	}

	function test(e) {
		console.log(e.detail);
	}

	function test2(e) {
		console.log(e.detail);
	}
</script>

<main>
	<Map on:test={test2}//>
	<YearSlider min="2009" max="2019" default="2012" on:year={test}/>
</main>
