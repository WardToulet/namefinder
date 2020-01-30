<script>
	export let placeList = {};

	let currentValue = '';

	let options = [];
	$: {
		for(let p in placeList) {
			options.push(placeList[p].Gemeente);
		}
		console.log(placeList);
	}
	/*let options = [*/
		/*'mechelen',*/
		/*'antwerpen',*/
		/*'brussel',*/
		/*'vilvoorde',*/
		/*'gent'*/
	/*];*/

	console.log(placeList);

	let display = false;

	$: updatedOptions = options.filter((v) => v.includes(currentValue)).sort().slice(0, 6);
	$: {
	}

	function onOptionClick(e) {
		currentValue = e.target.innerText;
		display = false;
	}

	function onEnter(e) {
		if(e.key === "Enter") {
			currentValue = updatedOptions.slice(0, 1);
		}
		display = false;
	}

	function displayNow() {
		display = true;
	}
</script>

<div class="autocomplete">
	<input type="text" on:keydown={onEnter} bind:value={currentValue} on:input={displayNow}/>
	
	{#if display}
		<div class="autocomplete-options">
			{#each updatedOptions as o}
				<div on:click={onOptionClick}>{ o }</div>
			{/each}
		</div>
	{/if}
</div>

<style>
	.autocomplete {
		display: inline-block;
		position: relative;
	}

	.autocomplete-options {
		position: absolute;
		border: 1px solid #d4d4d4;
		border-bottom: none;
		border-top: none;
		z-index: 99;
		top: 100%;
		left: 0;
		right: 0;
	}
	.autocomplete-options div {
		padding: 10px;
  		cursor: pointer;
  		background-color: #fff; 
  		border-bottom: 1px solid #d4d4d4; 
	}

	.autocomplete-options div:hover  {
		background: lightblue;
	}
</style>
