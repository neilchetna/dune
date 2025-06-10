<script lang="ts">
	import Grid from './Grid.svelte';
	import IconButton from '$lib/ui/button/IconButton.svelte';
	import GameOfLife from '$lib/ascii/GameOfLife.svelte';

	let isActive: boolean = $state(false);

	function toggleIsActive() {
		isActive = !isActive;
	}
</script>

<div class="header">
	<a href="/">
		<IconButton size="lg" icon="arrow-left" />
	</a>
	<GameOfLife />
</div>
<p class="subtext">
	<a class="external" target="_blank" href="https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life"
		>Conway's Game of Life</a
	> is a cellular automaton, a zero player game. It is played on a 2D square grid. Each square or cell
	on the grid can either be dead or alive. Toggle some cell by clicking on them and press play to see
	the cells evolve.
</p>
<div class="buttons">
	{#if !isActive}
		<IconButton size="xl" icon="play" onclick={toggleIsActive} />
	{:else}
		<IconButton size="xl" icon="pause" onclick={toggleIsActive} />
	{/if}
</div>

<Grid size={60} {isActive} />

<style>
	.header {
		display: flex;
		align-items: center;
		gap: 12px;
		margin: 12px auto;
		width: fit-content;
		text-shadow: 0 6px 10px rgba(0, 0, 0, 0.5);
		padding-right: 44px;
	}

	.subtext {
		margin: 12px auto;
		text-align: center;
		max-width: 80vmin;
	}

	.buttons {
		padding-top: 12px;
		margin: 0 auto;
		width: fit-content;
	}
</style>
