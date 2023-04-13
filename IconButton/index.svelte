<script>
	import { getContext, createEventDispatcher } from "svelte"
	import "../global.css"
	export const name = "Button"

	export let id
	export let classes = ""
	export let label = ""

</script>


	<button on:click
	on:mouseover
	on:mouseenter
	on:mouseleave
	on:focus {id} class="IconButton {classes}" label="{label}">
		<div class="contents">
			<slot />
		</div>
	</button>


<style>
	.IconButton {
		min-width: 30px;
    	height: 30px;
    	border: 2px solid transparent;
		position: relative;
		border-radius: 2px;
		/* margin: 2px -3px; */
	}

	.IconButton > .contents {
		position: absolute;
		top: 50%;
		left: 50%;
		pointer-events: none;
		transform: translate(-50%,-50%);
	}

	.IconButton:hover {
		background-color: var(--figma-color-bg-hover);
	}



	/* .secondary {
		background-color: transparent;
		color: var(--figma-color-text, black);
		border: 1px solid var(--figma-color-border-strong, white);
	} */

	/* .tertiary {
		background-color: transparent;
		color: var(--figma-color-text, black);
		border: 1px solid transparent;
	} */
</style>
