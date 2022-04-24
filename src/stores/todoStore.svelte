<script lang="ts" context="module">
    import { writable } from "svelte/store";

    export const todoList:any = writable([]);

    export const addTodo = (newItem:string) =>{
        if(newItem.trim() !== ""){
            todoList.update((curr:any) => {
                const newTodoList = [...curr, {todo: newItem, completed: false}];
                localStorage.setItem("todoList", JSON.stringify(newTodoList));
                return newTodoList;
            });
        }
    }

    export const removeTodo = (index:number) => {
        todoList.update((curr:any) => {
            curr = curr.filter((el:any, indextodo:number) => indextodo != index)
            localStorage.setItem("todoList", JSON.stringify(curr));
            return curr;
        });
    }

    export const todoToggleCompleted = (index:number) => {
        todoList.update((curr:any) =>{
            curr[index].completed = !curr[index].completed;
            localStorage.setItem("todoList", JSON.stringify(curr));
            return curr;
        });
    }
</script>