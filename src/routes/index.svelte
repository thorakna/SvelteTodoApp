<script lang="ts">
    import Icons from "../components/Icons.svelte";
    import { todoList, addTodo, removeTodo, todoToggleCompleted } from "../stores/todoStore.svelte";
    import { onMount } from "svelte";

    let newItem: string;

    onMount(()=>{
        const todoinLocal = localStorage.getItem("todoList");
        if(todoinLocal){
            todoList.update(() => JSON.parse(todoinLocal));
        }
    });
</script>

<svelte:head>
  <title>Welcome to Onur's Todo App</title>
</svelte:head>
<div>
    <form on:submit|preventDefault={()=>{
        addTodo(newItem);
        if(newItem.trim() !== "") newItem = "";
      }}>
      <input
        bind:value={newItem}
        type="text"
        class="bg-white w-72 px-4 py-2 rounded-md shadow-md placeholder-slate-400 focus:outline-none"
        placeholder="Enter a Todo!"
      />
      <button class="bg-sky-600 hover:bg-sky-500 transition-all px-4 py-2 rounded-md text-white font-bold shadow-md">+</button>
    </form>
    <a class="text-gray-300 ml-2 hover:text-gray-100 transition-all duration-500" href="/todoCounter">See statistics!</a>
</div>

<ul class=" h-4/6 overflow-y-auto">
{#each $todoList as item, index}
  <li class="bg-white rounded-md shadow-md w-96 px-4 py-2 m-3 flex flex-row">
    <span class="w-full {item.completed && `line-through`}">{item.todo}</span>
    <div class="flex flex-row">
        <button
          on:click={() => todoToggleCompleted(index)}
        >
          <Icons name={item.completed ? "check-mark-fill" : "check-mark"} class="icon" />
        </button>
  
        <button class="icon__button" on:click={() => removeTodo(index)}>
          <Icons name="delete" class="icon" />
        </button>
    </div>
  </li>
{/each}
</ul>