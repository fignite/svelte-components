<script>
  // import { getContext, createEventDispatcher } from "svelte"
  // import { valueStore } from "./data.js"
  // import { onMount } from "svelte"

  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let placeholder = "";
  export let value = "";
  export let label = "";
  export let disabled = false;
  export let id;
  export let type;
  export let min;
  export let max;
  export let step;
  export let classes = "";
  export let style;
  export let opts;
  export let icon;
  export let layout;
  export let fontWeight;

  function typeAction(node) {
    node.type = type;
  }
</script>

<div {style} class="Field layout-{layout} type-{type} font-weight-{fontWeight}">
  <label class={classes}>
    {#if layout === "stacked" || layout === "inline"}
      <span class="label">{label}</span>
    {/if}
    <div class="input layout-{layout}" data-value={value}>
      {#if type === "area"}
        <textarea
          on:input
          rows="4"
          {id}
          {disabled}
          bind:value
          placeholder={layout !== "stacked" ? placeholder : ""}
        />
      {:else}
        <input
          size="16"
          on:input
          on:focus
          use:typeAction
          autocomplete="false"
          {id}
          {disabled}
          placeholder={layout !== "stacked" ? placeholder : ""}
          bind:value
        />
      {/if}
    </div>
  </label>
</div>

<style>
  .font-weight-bold {
    font-weight: 600;
  }
  .layout-stacked .input,
  .layout-inline .input {
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

  /* Layout underline */

  .layout-underline .input {
    padding-left: 0;
    padding-right: 0;
    margin-left: 7px;
    margin-right: 7px;
    border-bottom: 1px solid var(--figma-color-border);
  }

  .layout-underline .input:hover {
    padding-left: 7px;
    padding-right: 7px;
    margin-left: 0;
    margin-right: 0;
  }

  .layout-underline .input:focus-within {
    padding-left: 6px;
    padding-right: 6px;
    margin-left: 0;
    margin-right: 0;
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
    padding-block: 1px;
  }

  .input {
    flex-basis: 100%;
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
    /* align-items: center; */
  }

  .layout-inline .label {
    margin: 0;
    margin-top: 7px; /* 6 + 1 to account for border */
  }

  .layout-inline label > :first-child {
    flex-basis: 80px;
    flex-shrink: 0;
  }

  .layout-inline label > :last-child {
    flex-grow: 1;
  }

  /* Type: area */

  .type-area .input {
    height: auto;
    padding: 0;
  }

  .type-area textarea {
    padding: 6px;
  }

  .type-area textarea:focus-within {
    padding: 5px;
  }

  .type-area textarea {
    border: none;
    width: 100%;
    background-color: transparent;
    font: inherit;
    resize: none;
    cursor: default;
  }

  .type-area textarea:focus-visible {
    /* border: none; */
    outline: none;
  }

  textarea {
    color: var(--figma-color-text);
  }

  .layout-grow .input {
    place-items: inherit !important;

    display: inline-grid;
    vertical-align: top;
    align-items: center;

    box-sizing: border-box;
  }
  .layout-grow .input input {
    width: auto;
    min-width: 1em;
    grid-area: 1/2;
  }
  .layout-grow .input::after {
    content: attr(data-value) " ";
    visibility: hidden;
    white-space: pre-wrap;

    width: auto;
    min-width: 1em;
    grid-area: 1/2;

    min-height: 1em;
    /* background-color: rgba(0, 0, 0, 0.1); */
  }
</style>
