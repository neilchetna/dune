<script lang="ts">
	const { size = 40 }: { size?: number } = $props();
	const blocks: number[][] = $state(new Array(size).fill(new Array(size).fill(0)));
	let currentRow: number = $state(0);

	function onBlockClick(i: number, j: number): void {
		blocks[i][j] = 1;
	}

	function falling(): void {
		if (currentRow == size) {
			currentRow = 0;
		}
		const i = currentRow;

		for (let j = 0; j < blocks.length; j++) {
			if (i === blocks.length - 1) {
				break;
			}

			if (!blocks[i][j]) {
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
		currentRow += 1;
	}

	$effect(() => {
		const interval = setInterval(() => {
			falling();
		}, 30);

		return () => {
			clearInterval(interval);
		};
	});
</script>

<section class="sandbox-root">
	<div class="sandbox" style:--size={size}>
		{#each blocks as vBlock, i}
			{#each vBlock as hBlock, j (`${i}-${j}`)}
				<button
					aria-label="sand-button"
					class:filled={hBlock}
					onmouseenter={() => onBlockClick(i, j)}
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
		border: 1px solid var(--color-fg-muted);
	}

	.filled {
		background-color: var(--color-fg);
	}
</style>
