<script>
	import { getContext, createEventDispatcher } from "svelte"
	import "../global.css"
	export const name = "Button"

	export let id
	export let classes = ""
	export let label = ""
	export let icon
	export let iconRight
	export let type

</script>


	<button on:preventDefault on:click
	on:mouseover
	on:mouseenter
	on:mouseleave
	on:focus {id} class="Button {classes}" label="{label}" {type}>
		<div class="gap">
		{#if icon}<span class="icon" icon={icon} />{/if}<span><slot /></span>{#if iconRight}<span class="icon" icon={iconRight} />{/if}
		</div>
	</button>


<style>
	.Button,
	button {
		line-height: 24px;
		padding: var(--padding-0) var(--padding-150);
		border: 2px solid var(--figma-color-bg-brand, var(--color-blue));
		background-color: var(--figma-color-bg-brand, var(--color-blue));
		color: white;
		border-radius: var(--border-radius-75);
		font-weight: 500;
		letter-spacing: 0.055px;
		overflow: hidden;
	}

	.Button {
		border-radius: var(--border-radius-75);
		display: flex;
		place-items: center;
	}

	.gap {
		gap: var(--size-50);
		display: flex;
		padding-block: 2px !important;
		place-items: center;
	}

	.icon {
		display: inline-block;
		width: 24px;
		height: 24px;
	}

	.secondary {
		background-color: transparent;
		color: var(--figma-color-text, black);
		border: 1px solid var(--figma-color-border-strong, white);
	}

	.tertiary {
		background-color: transparent;
		color: var(--figma-color-text, black);
		border: 1px solid transparent;
	}

	.danger {
		background-color: transparent;
		color: var(--figma-color-text-danger);
		border: 1px solid var(--figma-color-border-ondanger);
	}

	.tertiary2 {
		background-color: var(--figma-color-bg-tertiary);
		color: var(--figma-color-text, black);
		border: 1px solid transparent;
	}

	.Button.small {
		line-height: 20px;
		padding: var(--padding-0) 8px;
	}
</style>
