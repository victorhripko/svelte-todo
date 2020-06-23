<script>
  import { onMount } from 'svelte';
  import { nanoid } from 'nanoid';
  import { PlusIcon } from 'svelte-feather-icons';
  import Input from '../Input/Input.svelte';
  import TodoItem from './TodoItem.svelte';
  import { tasks } from '../../store.js';

	function updateStorage() {
    tasks.set(taskList);
	};

  let taskName = '';
  let taskList = $tasks;
  let dates = [];


  function createTask() {
    const d = new Date();
    const dateOptions = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };


    taskList = [{
      id: nanoid(),
      done: false,
      task: taskName,
      date: d.toLocaleDateString(undefined, dateOptions)
    }, ...taskList];

    dates = [...new Set(taskList.map(e => e.date))];
    updateStorage();

    console.log(taskList);
  };

  function fieldHandler(e) {
    if (e.key === 'Enter' && taskName) {
      createTask();
      e.target.value = taskName = '';
    }
  };

  function doneTask(event) {
    const id = event.detail;

    taskList = taskList.map(el => {
      return el.id === id ? {...el, done: !el.done} : el
    });

    updateStorage();
  };

  function removeTask(event) {
    const id = event.detail;

    taskList = taskList.filter(el => {
      return el.id !== id;
    });

    updateStorage();
  };
</script>

<div class="todo">
  <div class="todo__grid">
    <Input type="text" on:keydown={fieldHandler} bind:value={taskName} />
  </div>

  <div class="todo__list">
    {#each dates as date}
      {#if taskList.length > 0}
        <h5 class="todo__date">{date}</h5>
      {/if}
      {#each taskList as item (item.id)}
        {#if date === item.date}
          <TodoItem
            id={item.id}
            task={item.task}
            done={item.done}
            on:done={doneTask}
            on:remove={removeTask}
          />
        {/if}
      {/each}
    {/each}
  </div>
</div>

<style>
  .todo {
    padding: 2rem;
  }
  .todo__grid {
    padding-top: 2rem;
    padding-bottom: 2rem;
  }
  .todo__date {
    font-size: 5rem;
    color: black;
    margin-top: 1rem;
    margin-bottom: 2rem;
  }
  .todo__list {
    display: grid;
    row-gap: 2rem;
  }
</style>
