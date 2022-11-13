<script>
	import { activePanel } from '$lib/app';
	const time = '1:44am';
	const items = [
		{ displayText: 'Duplicate Media' },
		{ displayText: 'Executive' },
		{ displayText: 'GRiD 53' },
		{ displayText: 'GRiD 64' },
		{ displayText: 'GRiD 80' },
		{ displayText: 'GRiD Manager' },
		{ displayText: 'GRiDWrite' },
		{ displayText: 'Initialize Media' },
		{ displayText: 'MediaRepair' },
		{ displayText: 'Screen.Init' },
		{ displayText: 'User' }
	]

	let selection = 0;
	$: focused = activePanel === 'browser';
</script>

<svelte:window 
on:keydown={(e) => {
	if (focused) {
		if (e.key === 'ArrowDown') {
			selection++
		} else if (e.key === 'ArrowUp') {
			selection--
		}
		if (selection < 0) {
			selection = items.length;
		} else if (selection >= items.length) {
			selection = 0;
		}
	}
}}
/>

<div class="container" class:focused={focused} on:click={() => $activePanel === 'browser'}>
	<div class="items">
		{#each items as item, i}
		<button 
		class='item'
		class:selected={i === selection}
		on:click={() => selection = i }
		>
		{ item.displayText }
		</button>
		{/each}
	</div>
	<hr>
	<div class="console">
		hello
	</div>
</div>

<style>
	.container {
		display: grid;
		grid-template-rows: auto auto;
		border: 1px solid var(--orange-dim);
		padding: 1em;
		width: 200px;
	}
	.focused, .container:hover {
		border: 1px solid var(--orange);
	}
	.items {
		display: flex;
		flex-direction: column;
	}
	.item:hover:not(.selected) {
		color: white;
	}
	.selected {
		background-color: var(--orange);
		color: black;
	}
	hr {
		border: 1px solid var(--orange);
		width: 100%;
	}
	button {
		background-color: var(--black);
		border: 0;
		color: var(--orange);
		font-family: code;
		text-align: left;
	}
</style>

