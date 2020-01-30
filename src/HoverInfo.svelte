<script>
	import { fade } from 'svelte/transition';
	export let place;
	export let year;
</script>

<div>
	<h1 transition:fade>Place: {place !== null ? place.Gemeente : ''}</h1>
	<h1>Year: {year || ''}</h1>
</div>

