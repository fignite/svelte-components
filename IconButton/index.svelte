<script>
  import { getContext, createEventDispatcher } from "svelte";
  import "../global.css";
  export const name = "Button";

  export let id;
  export let classes = "";
  export let label = "";
  export let title;
</script>

<button
  on:click
  on:mouseover
  on:mouseenter
  on:mouseleave
  on:focus
  {id}
  class="IconButton {classes}"
  {label}
  {title}
>
  <div class="contents">
    <slot />
  </div>
</button>

<style>
  .IconButton {
    min-width: 32px;
    height: 32px;
    line-height: 32px;
    border: 1px solid transparent;
    background-clip: padding-box;
    position: relative;
    border-radius: 3px;
    /* margin: 2px -3px; */
    box-sizing: border-box;
  }

  .IconButton > .contents {
    position: absolute;
    top: 50%;
    left: 50%;
    pointer-events: none;
    transform: translate(-50%, -50%);
  }

  .IconButton:hover {
    background-color: var(--figma-color-bg-hover);
    /* Need this so that when other elements overlap, the one currently being hovered over stays on top */
    z-index: 100;
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
