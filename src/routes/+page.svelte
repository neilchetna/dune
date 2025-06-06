<script lang="ts">
	import '../app.css';
	import Sandbox from './Sandbox.svelte';
</script>

<pre class="header">
 ██████████                                 
░░███░░░░███                                
 ░███   ░░███ █████ ████ ████████    ██████ 
 ░███    ░███░░███ ░███ ░░███░░███  ███░░███
 ░███    ░███ ░███ ░███  ░███ ░███ ░███████ 
 ░███    ███  ░███ ░███  ░███ ░███ ░███░░░  
 ██████████   ░░████████ ████ █████░░██████ 
░░░░░░░░░░     ░░░░░░░░ ░░░░ ░░░░░  ░░░░░░  
</pre>
<h1>Sand Simulation</h1>
<div tabindex="0" role="grid" class="sandbox-container">
	<p>Drag you mouse across the canvas to add sand</p>
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
	}

	.sandbox-container {
		margin-top: 30px;
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
</style>
