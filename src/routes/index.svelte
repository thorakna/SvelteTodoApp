<script lang="ts">
    import Icons from "../components/Icons.svelte";
    import {writable} from "svelte/store";
    import { onMount } from "svelte";

    let newItem: string;
    const todoList:any = writable([]);

    onMount(()=>{
        const todoinLocal = localStorage.getItem("todoList");
        if(todoinLocal){
            todoList.update(() => JSON.parse(todoinLocal));
        }
    });

    const addTodo = () =>{
        if(newItem.trim() !== ""){
            todoList.update((curr:any) => {
                const newTodoList = [...curr, {todo: newItem, completed: false}];
                return newTodoList;
            });
            newItem = "";
        }
        localStorage.setItem("todoList", JSON.stringify($todoList));
    }

    const removeTodo = (index:number) => {
        todoList.update((curr:any) => curr.filter((el:any, indextodo:number) => indextodo != index));
        localStorage.setItem("todoList", JSON.stringify($todoList));
    }

    const todoToggleCompleted = (index:number) => {
        todoList.update((curr:any) =>{
            curr[index].completed = !curr[index].completed;
            return curr;
        });
        localStorage.setItem("todoList", JSON.stringify($todoList));
    }
</script>

<main class="container">
    <div>
        <form on:submit|preventDefault={addTodo}>
          <input
            bind:value={newItem}
            type="text"
            class="bg-white w-72 px-4 py-2 rounded-md shadow-md placeholder-slate-400 focus:outline-none"
            placeholder="Enter a Todo!"
          />
          <button class="bg-sky-600 hover:bg-sky-500 transition-all px-4 py-2 rounded-md text-white font-bold shadow-md">+</button>
        </form>
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
</main>

<style>
    .container{
        display:flex;
        flex-direction: column;
        align-items: center;
        max-width: 100vw;
        height: 100vh;
        background: #172241 no-repeat;
        background-size: cover;
        padding-top: 10vh;
    }
</style>