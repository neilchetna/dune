<script lang="ts">
	import { onMount } from 'svelte';
	const { size = 60, isMouseDown }: { size?: number, isMouseDown: boolean } = $props();
	const blocks: number[][] = $state(new Array(size).fill(new Array(size).fill(0)));
	let currentRow: number = $state(size - 1);

	function onBlockClick(i: number, j: number): void {
		blocks[i][j] = 1;
	}

	function loop(): void {
		if (currentRow < 0) {
			currentRow = size - 1;
		}
		let i = currentRow;
		const multiplyer = currentRow > 1 ? currentRow - 4 : 1;

		while (i >= 0 && i >= multiplyer) {
			for (let j = 0; j < blocks.length; j++) {
				if (!blocks[i][j] || i === size - 1) {
					continue;
				}

				if (blocks[i][j] && !blocks[i + 1][j]) {
					blocks[i][j] = 0;
					blocks[i + 1][j] = 1;
				}

				// Check Left
				if (blocks[i][j] && blocks[i + 1][j] && j > 0 && !blocks[i + 1][j - 1]) {
					blocks[i][j] = 0;
					blocks[i + 1][j - 1] = 1;
				}

				// Check Right
				if (blocks[i][j] && blocks[i + 1][j] && j < blocks.length - 1 && !blocks[i + 1][j + 1]) {
					blocks[i][j] = 0;
					blocks[i + 1][j + 1] = 1;
				}
			}
			i -= 1
		}

		currentRow -= 4;
		requestAnimationFrame(loop);
	}

	onMount(() => {
		loop();
	});
</script>

<section class="sandbox-root">
	<div class="sandbox" style:--size={size}>
		{#each blocks as vBlock, i}
			{#each vBlock as hBlock, j (`${i}-${j}`)}
				<button
					aria-label="sand-button"
					class:filled={hBlock}
					onmouseenter={() => isMouseDown && onBlockClick(i, j)}
					class="block"
				></button>
			{/each}
		{/each}
	</div>
</section>

<style>
	.sandbox-root {
		width: var(--box-size);
		height: var(--box-size);
		border: 1px solid var(--color-fg);
	}

	.sandbox {
		width: 100%;
		height: 100%;
		display: grid;
		grid-template-columns: repeat(var(--size), 1fr);
		grid-template-rows: repeat(var(--size), 1fr);
	}

	.block {
		all: unset;
		cursor: pointer;
	}

	.filled {
		background-color: var(--color-fg);
	}
</style>
