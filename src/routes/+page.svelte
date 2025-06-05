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
<h1>Sand Simulation 󱦟</h1>
<div class="sandbox-container">
	<Sandbox />
</div>

<style>
	h1,
	.header {
		width: fit-content;
		margin: 0 auto;
		font-family: var(--font-family, 'apple sans');
	}

	.header {
		margin-top: 2rem;
	}
	.sandbox-container {
		margin-top: 100px;
		width: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
	}
</style>
