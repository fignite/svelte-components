<script>
	// import { getContext, createEventDispatcher } from "svelte"
	// import { valueStore } from "./data.js"
	// import { onMount } from "svelte"

	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let placeholder = ""
	export let value = ""
	export let label = ""
	export let disabled = false
	export let id
	export let type
	export let min
	export let max
	export let step
	export let classes = ""
	export let style
	export let opts
	export let icon
	export let layout

	let input

	function typeAction(node) {
		node.type = type;
	}
	
</script>

<div style={style} class="Field layout-{layout}">
	
	<label class="{classes}">
		{#if layout === "stacked" || layout === "inline"}
			<span class="label">{label}</span>
		{/if}
		<div class="input">
			<input use:typeAction autocomplete="false"
				{id}
				{disabled}
				placeholder={layout !== "stacked" ? placeholder : ""}
				bind:value />
		</div>
	</label>
</div>

<style>

	.layout-stacked .input, .layout-inline .input {
		border: 1px solid var(--figma-color-border);
	}

	div {
		padding-block: 2px;
	}
	.input {
		display: flex;
		border: 1px solid transparent;
		place-items: center;
		height: 28px;
		/* margin-left: calc(
			var(--fgp-gap_item_column, 0px) + (-1 * var(--margin-100))
		); */
		/* margin-right: calc((-1 * var(--margin-100))); */
		padding-inline: 7px;
		border-radius: var(--border-radius-25);
	}

	.input:hover {
		border-color: var(--figma-color-border, var(--color-black-10));
		border-width: 1px;
		padding-inline: 7px;
	}

	.input:focus-within {
		border-color: var(--figma-color-border-selected, var(--color-blue));
		border-width: 2px;
		padding-inline: 6px;
	}

	.input span {
		/* margin-right: var(--margin-200); */
		color: var(--figma-color-text-tertiary, var(--color-black-30));
		min-width: 32px;
		text-align: center;
		margin-left: -8px;
	}

	.input input {
		flex-grow: 1;
		cursor: default;
		width: 50px;
	}

	.label {
		display: block;
		margin-bottom: 4px;
		font-weight: 500;
	}

	input[disabled] {
		color: var(--figma-color-text-disabled);
	}

	.layout-inline label {
		display: flex;
		align-items: center;
	}

	.layout-inline label > :first-child {
		flex-basis: 100px;
	}

	.layout-inline label > :last-child {
		flex-grow: 1;
	}
</style>
