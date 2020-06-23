<script>
  import { createEventDispatcher } from 'svelte';
  import { CheckIcon, Trash2Icon } from 'svelte-feather-icons';
  import Button from '../Button/Button.svelte';


  const dispatch = createEventDispatcher();

  export let id;
  export let task;
  export let done;

  function markDone() {
    dispatch('done', id);
  };

  function remove() {
    dispatch('remove', id);
  };
</script>

<div class={done ? `todo__task todo__task--done` : `todo__task` }>
  <div class="todo__block">
    <Button on:click={markDone} active={done} class="todo__btn" accent="#4834d4">
      <CheckIcon size="1x" />
    </Button>
    <p class="todo__text">
      {task}
    </p>
  </div>

  <Button on:click={remove} accent="red">
    <Trash2Icon size="1x" />
  </Button>
</div>

<style>
  .todo__task {
    position: relative;
    display: grid;
    grid-template-columns: 1fr min-content;
    align-items: center;
    column-gap: 2rem;
  }

  .todo__block {
    display: flex;
    align-items: center;
    padding: 1rem;
    box-shadow: 0 0 2rem 0 rgba(200, 200, 200, .5);
    border-radius: .6rem;
    border-width: .2rem;
    border-style: solid;
    border-color: transparent;
    background-color: white;
  }

  :global(.todo__btn) {
    margin-right: 2rem;
  }

  .todo__text {
    margin: 0;
    flex: 1 1 auto;
    font-size: 1.8rem;
    line-height: 1.6;
    font-family: inherit;
    color: black;
  }

  .todo__task--done .todo__block {
    background-color: rgba(255, 255, 255, .1);
     box-shadow: 0 0 2rem 0 rgba(200, 200, 200, .1);
  }

  .todo__task--done .todo__text {
    text-decoration: line-through;
    opacity: .5;
  }

</style>
