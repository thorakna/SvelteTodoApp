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

<svelte:head>
  <title>See your statistics! - Onur's Todo App</title>
</svelte:head>

<div class=" bg-sky-600 bg-opacity-50 rounded-md w-full md:w-2/3 overflow-hidden shadow-md px-4 py-2 text-gray-50">
  <h3 class="text-xl text-neutral-200">Statistics!</h3>
  You have {$todoList.length} todo!
</div>