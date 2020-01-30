<script>
	import Map from './Map.svelte';
	import YearSlider from './YearSlider.svelte';
	import HoverInfo from './HoverInfo.svelte';
	import Stats from './Stats.svelte';
	import Graphs from './Graphs.svelte';
	import Test from './Test.svelte';

	let namesByYearByPlace = null; 
	fetch(`./data/byYearByPlace.json`)
		.then(res => res.json())
		.then(obj => {
			namesByYearByPlace = obj
			console.log(obj);
		});

	let placeNameById = null;
	fetch(`./data/gemeenten.json`)
		.then(res => res.json())
		.then(obj => {
			placeNameById = obj;
			console.log(obj);
		});

	let year = 2009;
	let placeId = null;
	let hoverPlace = null;

	let names = null;
	$: { 
		if(year !== null 
			&& placeId !== null && namesByYearByPlace !== null 
			&& namesByYearByPlace[year] !== null)
		{
			names = namesByYearByPlace[year][placeId];
			console.log(names);
		}
	}

	function setYear(e) {
		year = e.detail.year;
	}

	function selectPlace(e) {
		placeId = e.detail.id;
	}

	function focus(e){
		e.target.style.fill = 'blue';

	}

	function hoverOn(e) {
		if(placeNameById !== null && placeNameById[e.detail.id])
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
	{#if names != null}
		<Graphs bind:nameList={names} />
	{/if}
</main>
