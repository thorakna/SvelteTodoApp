<script lang="ts">
  import { todoList } from "../stores/todoStore.svelte";
  import {onMount} from "svelte"; 
  onMount(()=>{
      const todoinLocal = localStorage.getItem("todoList");
      if(todoinLocal){
          todoList.update(() => JSON.parse(todoinLocal));
      }
  });
</script>

<main class="container">
  <h2 class=" text-sky-500 font-bold text-2xl mb-5">Onur's Todo List</h2>
  <div class=" bg-sky-600 bg-opacity-50 rounded-md w-full md:w-2/3 overflow-hidden shadow-md px-4 py-2 text-gray-50">
    You have {$todoList.length} todo!
  </div>
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
        padding-top: 2vh;
        padding-left: 2vw;
        padding-right: 2vw;
    }
</style>