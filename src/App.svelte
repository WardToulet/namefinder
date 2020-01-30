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
	let mNames = names.filter(e => e.gender == "M");
	let fNames = names.filter(e => e.gender == "F");

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
	<div style="float: left; width: 60%;"> <!-- Doe dit met grids als ge dat liever ziet -->
		<HoverInfo year={year} place={hoverPlace} />
		<Map on:selectPlace={selectPlace} on:hoverOfPlace={hoverOff} on:hoverOnPlace={hoverOn}/>
		<YearSlider min="2009" max="2019" on:year={setYear}/>
		<Stats names={names}/>
	</div>

	<div id="Graphs" style="float: right; width 40%;"><!-- Same -->
		{#if fNames != null && mNames != null}
			<Graphs bind:nameList={fNames} gender="F"/>
			<Graphs bind:nameList={mNames} gender="M"/>
		{/if}
	</div>
</main>
