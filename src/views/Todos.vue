<template>
  <div>
    <h1>Todos</h1>
    <div v-for="(todo, index) in todos"
      :key="index">
      {{todo.text}} 
      <br /> 
      <button @click="removeTodo(index)" title="Remove todo">&times;</button>
      <button v-if="!todo.done" @click="markAsDone(index)" title="Mark as done">&check;</button>
      <button v-if="todo.done" @click="markAsUndone(index)" title="Mark as undone">&#8630;</button>
      <br />
      {{todo.createdAt.toString()}}
    </div>
    <div v-if="todos.length ===0">
      You don't have any task to do.
    </div>
    <div>
      <h2>Add a To-do</h2>
      <input type="text"
        v-model="todoText"
        @keydown.enter="addTodo">
    </div>
  </div>
</template>

<script>
import { defineComponent, reactive, ref } from "vue";

export default defineComponent({
  setup() {
    const todos = reactive([]);
    const todoText = ref(""); // ref stores data as an object with 'value' as key

    function addTodo() {
      todos.unshift({
        text: todoText.value,
        createdAt: new Date().toLocaleString(),
        done: false        
      });
     todoText.value = "";
    }
    
    function markAsDone(index){
      todos[index].done = true;
    }

    function markAsUndone(index){
      todos[index].done = false;
    }

    function removeTodo(index) {
      if(!confirm("Are you sure?")){
        return;
      }
        todos.splice(index,1);
        alert('removed');
      
    }

    return {
      todos,
      todoText,
      addTodo,
      markAsDone,
      markAsUndone,
      removeTodo
    };
  }
});
</script>