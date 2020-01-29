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

	function hoverOn(e) {
		console.log('hover');
	}

	function hoverOff(e) {
		console.log('no hover');	
	}
</script>

<main>
	<Map on:selectPlace={test2} on:hoverOfPlace={hoverOn} on:hoverOnPlace={hoverOn}/>
	<YearSlider min="2009" max="2019" on:year={test}/>
</main>
