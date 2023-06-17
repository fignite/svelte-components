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
  export let togglePassword;

  function typeAction(node) {
    node.type = type;
  }

  function togglePasswordView() {
    if (input.type === "password") {
      input.type = "text";
    } else {
      input.type = "password";
    }
  }

  let input;
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
          bind:this={input}
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
        {#if togglePassword}
          <span
            class="check-toggle"
            on:click={() => {
              togglePasswordView();
            }}
          >
            {#if input && input.type === "text"}
              <svg
                width="16"
                height="16"
                viewBox="0 0 16 16"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <g clip-path="url(#clip0_0_17552)">
                  <path
                    fill-rule="evenodd"
                    clip-rule="evenodd"
                    d="M8.00019 11C5.70033 11 3.67803 9.80581 2.52182 8C3.67803 6.19419 5.70033 5 8.00019 5C10.3 5 12.3223 6.19419 13.4785 8C12.3223 9.80581 10.3 11 8.00019 11ZM8.00019 4C10.8782 4 13.3776 5.6211 14.6351 8C13.3776 10.3789 10.8782 12 8.00019 12C5.12214 12 2.62273 10.3789 1.36523 8C2.62273 5.6211 5.12214 4 8.00019 4ZM8.00049 10C9.10506 10 10.0005 9.10457 10.0005 8C10.0005 6.89543 9.10506 6 8.00049 6C6.89592 6 6.00049 6.89543 6.00049 8C6.00049 9.10457 6.89592 10 8.00049 10Z"
                    fill="currentColor"
                    fill-opacity="0.8"
                  />
                </g>
                <defs>
                  <clipPath id="clip0_0_17552">
                    <rect width="16" height="16" fill="white" />
                  </clipPath>
                </defs>
              </svg>
            {/if}

            {#if input && input.type === "password"}
              <svg
                width="16"
                height="16"
                viewBox="0 0 16 16"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <g clip-path="url(#clip0_0_17556)">
                  <path
                    fill-rule="evenodd"
                    clip-rule="evenodd"
                    d="M13.5085 7.80119C14.0639 7.27364 14.5436 6.66723 14.9295 6H13.7453C12.4798 7.81421 10.378 9 7.99986 9C5.62172 9 3.51992 7.81421 2.25446 6H1.07022C1.45619 6.66728 1.93589 7.27373 2.49134 7.80131L0.896484 9.39623L1.6036 10.1033L3.26094 8.44592C3.97166 8.96931 4.77213 9.37804 5.63506 9.64469L5.01804 11.866L5.98156 12.1336L6.60775 9.87929C7.05984 9.95862 7.52501 10 7.99986 10C8.47467 10 8.9398 9.95863 9.39185 9.87931L10.018 12.1336L10.9816 11.866L10.3646 9.64473C11.2276 9.37806 12.0281 8.96928 12.7389 8.44582L14.3965 10.1033L15.1036 9.39621L13.5085 7.80119Z"
                    fill="currentColor"
                    fill-opacity="0.8"
                  />
                </g>
                <defs>
                  <clipPath id="clip0_0_17556">
                    <rect width="16" height="16" fill="white" />
                  </clipPath>
                </defs>
              </svg>
            {/if}
          </span>
        {/if}
      {/if}
    </div>
  </label>
</div>

<style>
  .check-toggle {
    display: block;
    min-width: auto !important;
    padding: 8px;
    margin: -8px;
  }
  .check-toggle:hover svg path {
    fill-opacity: 1;
    fill: var(--figma-color-text-secondary);
  }
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
