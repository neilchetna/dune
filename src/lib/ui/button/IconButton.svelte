<script lang="ts">
	import type { Icon } from '$lib/icons';
	import type { HTMLButtonAttributes } from 'svelte/elements';

	type Size = 'sm' | 'md' | 'lg' | 'xl';
	interface Props {
		icon: Icon;
		size: Size;
	}

	const { icon, size = 'md', class: styleClass, ...rest }: Props & HTMLButtonAttributes = $props();

	const sizeMap: Record<Size, string> = {
		sm: '12px',
		md: '24px',
		lg: '32px',
		xl: '60px'
	};
</script>

<button style:--size={sizeMap[size]} class="icon-button {styleClass}" aria-label={icon} {...rest}>
	<span style:--size={sizeMap[size]} class="icon {icon}"></span>
</button>

<style>
	.icon-button {
		all: unset;
		height: var(--size, 24px);
		width: var(--size, 24px);
		background-color: rgba(255, 255, 255, 0.2);
	}
	.icon {
		height: var(--size, 24px);
		width: var(--size, 24px);
		display: inline-block;
		background-repeat: no-repeat;
		background-size: 100% 100%;
	}
</style>
