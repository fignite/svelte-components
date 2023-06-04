<script>
  import { getContext, createEventDispatcher } from "svelte";
  import "../global.css";
  export const name = "Button";

  export let id;
  export let classes = "";
  export let label = "";
  export let icon;
  export let iconRight;
  export let type;
</script>

<button
  on:preventDefault
  on:click
  on:mouseover
  on:mouseenter
  on:mouseleave
  on:focus
  {id}
  class="Button {classes}"
  {label}
  {type}
>
  <div class="gap">
    {#if icon}<span class="icon" {icon} />{/if}<span><slot /></span
    >{#if iconRight}<span class="icon" icon={iconRight} />{/if}
  </div>
</button>

<style>
  .Button,
  button {
    line-height: 22px;
    padding: var(--padding-0) 11px;
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
    line-height: 24px;
    background-color: transparent;
    color: var(--figma-color-text, black);
    border: 1px solid var(--figma-color-border-strong, white);
  }

  .ghost {
    line-height: 24px;
    background-color: transparent;
    color: var(--figma-color-text, black);
    border: 1px solid transparent;
  }

  .ghost:hover {
    background-color: var(--figma-color-bg-hover);
  }

  .tertiary {
    line-height: 24px;
    background-color: transparent;
    color: var(--figma-color-text, black);
    border: 1px solid transparent;
  }

  .danger {
    line-height: 24px;
    background-color: transparent;
    color: var(--figma-color-text-danger);
    border: 1px solid var(--figma-color-border-ondanger);
  }

  .tertiary2 {
    line-height: 24px;
    background-color: var(--figma-color-bg-tertiary);
    color: var(--figma-color-text, black);
    border: 1px solid transparent;
  }

  .Button.small {
    line-height: 20px;
    padding: var(--padding-0) 8px;
  }

  .Button:enabled:active,
  .Button:enabled:focus {
    padding: 0 10px;
    border: 2px solid var(--figma-color-border-selected);
  }

  .Button:enabled:active .gap,
  .Button:enabled:focus .gap {
    padding-block: 1px !important;
  }
</style>
