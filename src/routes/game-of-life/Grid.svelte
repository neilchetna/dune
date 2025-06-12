<script lang="ts">
	import duneArt from '$lib/images/dune-art-pixel.png';

	const { size = 40, isActive = false }: { size: number; isActive: boolean } = $props();
	const grid: number[][] = $state(new Array(size).fill(new Array(size).fill(0)));
	const fossilGrid: number[][] = $state(new Array(size).fill(new Array(size).fill(0)));

	const loop = () => {
		if (!isActive) {
			return;
		}

		const prevGrid = grid.map((row) => row.slice());
		for (let i = 0; i < size; i++) {
			for (let j = 0; j < size; j++) {
				let count = 0;

				if (j < size - 1) {
					count += prevGrid[i][j + 1];

					if (i < size - 1) {
						count += prevGrid[i + 1][j + 1];
					}

					if (i > 0) {
						count += prevGrid[i - 1][j + 1];
					}
				}

				if (j > 0) {
					count += prevGrid[i][j - 1];

					if (i < size - 1) {
						count += prevGrid[i + 1][j - 1];
					}

					if (i > 0) {
						count += prevGrid[i - 1][j - 1];
					}
				}

				if (i > 0) {
					count += prevGrid[i - 1][j];
				}

				if (i < size - 1) {
					count += prevGrid[i + 1][j];
				}

				if (!prevGrid[i][j] && count == 3) {
					grid[i][j] = 1;
					fossilGrid[i][j] = 1;
					continue;
				}

				if (count < 2 || count > 3) {
					grid[i][j] = 0;
				}
			}
		}
	};

	$effect(() => {
		const id = setInterval(() => loop(), 100);

		return () => clearInterval(id);
	});

	const handleOnDraw = (i: number, j: number) => {
		grid[i][j] = +!grid[i][j];
	};
</script>

<div class="grid-container" style:--size={size}>
	{#each grid as row, i (i)}
		{#each row as cell, j (`${i},${j}`)}
			<button
				aria-label="button to toggle state of the cell ({i}, {j})"
				class:filled={cell}
				class:fossil={fossilGrid[i][j] && !cell}
				class="cell"
				onclick={() => handleOnDraw(i, j)}
			></button>
		{/each}
	{/each}
	<div class="dune-wrapper">
		<img class="dune" src={duneArt} alt="sand dune" />
	</div>
</div>

<style>
	.grid-container {
		position: relative;
		width: 75vmin;
		height: 75vmin;
		margin: 0 auto;
		margin-top: 24px;

		background-color: var(--color-fg-alt);

		font-size: 8px;

		display: grid;
		grid-template-columns: repeat(var(--size), 1fr);
		grid-template-rows: repeat(var(--size), 1fr);
	}

	.cell {
		all: unset;
		user-select: none;
		border: 1px solid var(--color-fg-2-muted);
	}

	.filled {
		background-color: var(--color-fg-3);
	}

	@keyframes colorFade {
		0% {
			background-color: var(--color-bg);
		}
		100% {
			background-color: transparent;
		}
	}

	.fossil {
		opacity: 90%;
		animation: colorFade 15s forwards;
	}

	.dune-wrapper {
		position: absolute;
		display: flex;
		align-items: center;
		bottom: 0;
		opacity: 0.3;
		pointer-events: none;
	}

	.dune {
		margin: 0 auto;
		width: 75vmin;
	}
</style>
