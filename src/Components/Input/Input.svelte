<script>
  export let type = 'text';
  export let value = '';
  export let placeholder = null;
  export let disabled = false;
</script>

<input
  class="input"
  {type}
  {placeholder}
  tabindex={ disabled ? -1 : null }
  on:keydown
  on:input={e => value = e.target.value}
/>

<style>
  .input {
    display: block;
    width: 100%;
    min-width: 0;
    height: 5rem;
    padding: .5rem 1.5rem;
    border-width: .2rem;
    border-style: solid;
    border-color: transparent;
    font-family: inherit;
    font-size: 1.8rem;
    background-color: white;
    color: black;
    border-radius: .6rem;
    line-height: 0;
    box-shadow: 0 0 2rem 0 rgba(200, 200, 200, .5);
    outline: none;
  }

  .input:hover,
  .input:focus {
    border-color: black;
  }

  .input:disabled {
    opacity: .5;
    pointer-events: none;
  }
</style>
