<script>
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher(); 
	export let min;
	export let max;
	export let def = Integer(min + ((max - min) / 2));

	function changeYear(e) {
		dispatch('year', {
			year: e.target.value
		});	
	}
</script>

<input id="year_inp" 
       type="range" 
       name="year_inp"
       min={min}
       max={max}
       value={def}
       on:input={changeYear}
>
