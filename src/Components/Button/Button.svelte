<script>
  export let active = false;
  export let disabled = false;
  export let className = '';
  export let accent = 'black';

  let classDefault = className ? `${className} button` : 'button';

  export { className as class }
</script>

<button
  class="{ active && !disabled ? `${classDefault} button--active` : classDefault }" {disabled}
  on:click|stopPropagation
  tabindex={ disabled ? -1 : null }
  style="--button-color: {accent}"
>
  <slot />
</button>

<style>
  .button {
    position: relative;
    display: block;
    min-width: 5rem;
    height: 5rem;
    padding: .5rem 1rem;
    border-width: .2rem;
    border-style: solid;
    border-color: transparent;
    font-family: inherit;
    font-size: 2.2rem;
    background-color: white;
    color: var(--button-color);
    border-radius: .6rem;
    line-height: 0;
    cursor: pointer;
    outline: none;
    box-shadow: 0 0 2rem 0 rgba(180, 180, 180, .4);
  }

  .button:hover,
  .button:focus {
    border-color: var(--button-color);
  }

  .button--active {
    background-color: var(--button-color);
    color: white;
  }

  .button--active:hover {
    border-color: white;
  }

  .button:disabled {
    opacity: .5;
    pointer-events: none;
  }
</style>
