<script context="module">
  const dropdowns = {};

  export function getDropdown(id = "") {
    return dropdowns[id];
  }
</script>

<script>
  import { onDestroy } from "svelte";

  export let showMenu = false;
  export let id = "";
  export let style;
  export let fill;
  export let expandOnHover;
  export let showBorder;

  function clickOutside(element, callbackFunction) {
    function onClick(event) {
      if (!element.contains(event.target)) {
        callbackFunction(event, element);
      }
    }

    document.body.addEventListener("click", onClick);

    return {
      update(newCallbackFunction) {
        callbackFunction = newCallbackFunction;
      },
      destroy() {
        document.body.removeEventListener("click", onClick);
      },
    };
  }

  function close() {
    showMenu = false;
  }

  function open() {
    showMenu = true;
  }

  dropdowns[id] = { open, close };

  onDestroy(() => {
    delete dropdowns[id];
  });
</script>

<div
  {style}
  class="host Select {showMenu ? 'show' : ''} {fill
    ? 'fill'
    : ''} {expandOnHover ? 'expandOnHover' : ''} {showBorder
    ? 'showBorder'
    : ''}"
  use:clickOutside={(event, element) => {
    close();
  }}
>
  {#if $$slots.hitThing}
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div
      on:click={(event) => {
        if (showMenu === false) {
          open();
        } else {
          close();
        }

        window.addEventListener("blur", () => {
          // parentElement.classList.remove("show")
          close();
        });
      }}
    >
      <slot name="hitThing" />
    </div>
  {/if}

  {#if $$slots.label}
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div
      class="label"
      on:click={(event) => {
        if (showMenu === false) {
          open();
        } else {
          close();
        }

        window.addEventListener("blur", () => {
          // parentElement.classList.remove("show")
          close();
        });
      }}
    >
      {#if $$slots.icon}<span class="label-icon"><slot name="icon" /></span
        >{/if}
      <span class="text"><slot name="label" /></span>

      <span class="" style="margin-left: 8px">
        <div class="icon figma-light">
          <svg
            width="8"
            height="8"
            viewBox="0 0 8 8"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path opacity="0.30" d="M1 2.5L4 5.5L7 2.5" stroke="black" />
          </svg>
        </div>
        <div class="icon figma-dark">
          <svg
            width="8"
            height="8"
            viewBox="0 0 8 8"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path opacity="0.30" d="M1 2.5L4 5.5L7 2.5" stroke="white" />
          </svg>
        </div>
      </span>
    </div>
  {/if}
  <div class="content">
    <slot name="content" />
  </div>
</div>

<style>
  .Select {
    padding: 1px;
  }
  .Select > .label {
    /* line-height: 1; */
    border: 2px solid transparent;
    place-items: center;
    min-height: 30px;
    /* margin-left: calc(
			var(--fgp-gap_item_column, 0px) + (-1 * var(--margin-100))
		); */
    /* margin-right: calc((-1 * var(--margin-100))); */
    padding-inline: calc(var(--padding-100) - 2px);
    border-radius: var(--border-radius-25);
    position: relative;
    display: flex;
    place-items: center;
    /* min-height: 30px; */
    cursor: default;
  }

  .Select:hover svg path {
    opacity: 0.8;
  }

  .Select.show svg path {
    opacity: 0.8;
  }

  .Select:hover > .label {
    /* padding-top: 1px; */
    border-color: var(--figma-color-border, var(--color-black-10));
    border-width: 1px;
    padding-inline: calc(var(--padding-100) - 1px);
  }

  .Select.showBorder .label {
    /* padding-top: 1px; */
    border-color: var(--figma-color-border, var(--color-black-10));
    border-width: 1px;
    padding-inline: calc(var(--padding-100) - 1px);
  }

  .Select > .label > .icon:first-child {
    margin-left: calc((-1 * var(--margin-50)));
    margin-right: var(--margin-25);
  }

  .Select.show > .label {
    border-color: var(--figma-color-border, var(--color-black-10));
    border-width: 1px;
    padding-inline: calc(var(--padding-100) - 1px);
  }

  /* .Select:not(.fill) > .label {
		max-width: 120px;
	} */

  .Select:not(.fill) > .label > span {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .Select.fill {
    flex-grow: 1;
  }

  .Select.fill > .label {
    margin-right: 0;
  }

  .Select.fill:hover > .label > [icon="chevron-down"] {
    margin-left: auto !important;
  }

  .Select.fill.show > .label > [icon="chevron-down"] {
    margin-left: auto !important;
  }

  .show > .tooltip {
    display: block;
  }

  .host {
    /* display: flex; */
  }

  .host .text {
    display: flex;
    gap: 8px;
  }

  .host .label {
    display: flex;
  }

  .host .content {
    display: none;
    position: absolute;
  }

  .host.show .content {
    display: block;
    z-index: 100;
  }

  /* expandOnHover */

  .host.expandOnHover:hover {
    flex-grow: 1;
  }

  .host.expandOnHover:hover .label .text {
    flex-grow: 1;
  }
  .label-icon {
    margin-right: 8px;
  }
</style>
