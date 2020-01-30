<script>
	export let names;
	$: top10 = names != null ? names.sort((x1, x2) => x1.count < x2.count).slice(0, 9) : [];
</script>

<ul>
{#each top10 as name}
	<li>{name.name} {name.count}</li>
{/each}
</ul>
