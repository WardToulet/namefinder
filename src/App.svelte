<script>
	import Map from './Map.svelte';
	import YearSlider from './YearSlider.svelte';
	import HoverInfo from './HoverInfo.svelte';
	import Stats from './Stats.svelte';

	let namesByYearByPlace = null; 
	fetch(`./data/byYearByPlace.json`)
		.then(res => res.json())
		.then(obj => {
			namesByYearByPlace = obj
			console.log(namesByYearByPlace);
		});

	let placeNameById = null;
	fetch(`./data/gemeenten.json`)
		.then(res => res.json())
		.then(obj => placeNameById = obj);

	let year = 2009;
	let place = null;
	let placeId = null;
	let hoverPlace = null;

	let names = [];

	async function getJSON(name) {
		let res = await fetch(`./data/${name}.json`);
		let obj = await res.json();

		console.log(obj);

		if(!res.ok)
			return new Error(obj);

		return obj;
	}

	function setYear(e) {
		year = e.detail.year;
	}

	function selectPlace(e) {
		if(placeNameById != null && placeNameById[e.detail.id])
			names =	namesByYearByPlace[year][e.detail.id].sort((a, b) => a.name > b.name);
	}

	function hoverOn(e) {
		if(placeNameById != null && placeNameById[e.detail.id])
			hoverPlace = placeNameById[e.detail.id];
	}

	function hoverOff(e) {
		hoverPlace = null;
	}
</script>

<main>
	<HoverInfo year={year} place={hoverPlace} />
	<Map on:selectPlace={selectPlace} on:hoverOfPlace={hoverOff} on:hoverOnPlace={hoverOn}/>
	<YearSlider min="2009" max="2019" on:year={setYear}/>
	<Stats names={names}/>
</main>
