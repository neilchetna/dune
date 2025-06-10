<script lang="ts">
	import Dune from '$lib/ascii/Dune.svelte';
	import Sandbox from './Sandbox.svelte';
</script>

<div class="header">
	<Dune />
</div>
<ul class="navbar">
	<li class="nav-link"><a href="/game-of-life">Game Of Life</a></li>
</ul>
<h1>Sand Simulation</h1>
<div class="sandbox-container">
	<p class="subtext">Drag you mouse across the canvas to add sand</p>
	<Sandbox />
</div>

<style>
	h1,
	.header {
		width: fit-content;
		margin: 0 auto;
	}

	.header {
		margin-top: 2em;
		font-size: 12px;
		text-shadow: 0 6px 10px rgba(0, 0, 0, 0.3);
	}

	.navbar {
		display: flex;
		justify-content: center;
		list-style-type: none;
		width: 100%;
		gap: 2rem;
		padding: 0;
	}

	.nav-link {
		width: fit-content;
		text-align: center;
	}

	.sandbox-container {
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.subtext {
		margin-top: 4px;
	}
</style>
