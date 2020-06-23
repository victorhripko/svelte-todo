<script>
  import Todo from './Components/Todo/Todo.svelte';
  import { onMount } from 'svelte';
  import { tasks } from './store.js';

  $: taskDoneCount = $tasks.filter(e => e.done).length;

</script>

<div class="app">
  <div class="app__main">
    <Todo />
  </div>
  <aside class="app__aside">
    {#if $tasks.length > 0}
      Count: {$tasks.length}&nbsp;&nbsp;Done: {taskDoneCount}
    {/if}
  </aside>
</div>

<style>
  .app {
    height: 100%;
    display: grid;
    grid-template-columns: 60% 40%;
    grid-template-areas: "main aside";
  }
  .app__main {
    grid-area: main;
    overflow-y: auto;
  }
  .app__aside {
    grid-area: aside;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    font-size: 2vw;
  }
</style>
