<script setup>

</script>

<template>
  <div>
<div><p class="text-center text-4xl mt-4 font-bold font-mono">{{ title }}</p></div>

<div class="todo">
  <input type="" v-model="text" placeholder="todo" class="outline-none border">
  <button @click="addTodo(id++)">add todo</button>
  <div class="bg-gray-100 w-[300px]" v-for="(todo,) in todos" :key="todo.id">
    <p class="flex gap-10">  
      <span class="todo__id">{{ todo.id +1 }}</span>
  
      <span  v-if="!editting"  class="todo__text " :class="{todo__text_isDone:isDone}" >{{ todo.text }}</span>
      <input v-bind:value="editText" @change="editTextChange" v-else type="text">
      <input type="checkbox" class="inline-block todo_check" v-model="isDone" >
      <button @click="deleteTodo(todo.id)">delete</button>
      <button @click="editTodo(todo)">{{editting?"update":"edit"}}</button>
    
    </p>
 

  </div>

</div>
  </div>
</template>
<script>
import {mapActions} from "vuex"
export default {
  data(){
    return {
      title:"Todo app",
      text:"",
      todos:[],
      isDone:false,
      id:0,
      editting:false,
      editText:""
    }
  },
  methods:{
    addTodo(){
      this.todos.push({
        id:this.id,
        text:this.text,
        done:this.isDone
    }),
      this.todo=""
    },

   }
 
    
  }
}
</script>
<style lang="scss">
.todo{
  border: 2px solid gray;
  &__text{
 &_isDone{
  text-decoration: line-through;
 }
  }

}

</style>

