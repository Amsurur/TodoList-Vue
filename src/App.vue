

<script setup>

</script>

<template>
  
  <div>
<div><p class="text-center text-4xl mt-4 font-bold font-mono">{{ title }}</p></div>

<div class="">
  <div class="justify-center mt-10 flex gap-5">
  <input type="" v-model="text" placeholder="I can do" class="outline-none w-[420px] h-[40px] rounded-lg px-3 border border-green-500 ">
  <button @click="addTodo(id++)" class="bg-green-400 w-[100px] text-white h-[40px] rounded-lg" >Add</button>
</div>
  <div class="bg-gray-100  border-red-400 border rounded-lg px-2 w-[35%]  mt-2 mx-auto  " v-for="(todo,) in todos" :key="todo.id">
    <div class="flex justify-center items-center p-2 gap-10 ">  
      <span class="todo__id bg-orange-300  text-center px-2  rounded-xl"  >{{ todo.id }}</span>
  
      <span  v-if="!editting"  class="todo__text " :class="{todo__text_isDone:isDone}" >{{ todo.text }}</span>
      <input v-bind:value="editText" @change="editTextChange" v-else type="text">
      <div  class="flex items-center gap-2">
      <input type="checkbox" class="inline-block todo_check" v-model="isDone" >
      <button @click="deleteTodo(todo.id)" class="bg-red-400 px-2 text-white rounded">delete</button>
      <button @click="editTodo(todo)" class="bg-purple-400 px-2 text-white rounded">{{editting?"update":"edit"}}</button>
    </div>
    </div>
 

  </div>

</div>
  </div>
</template>
<script>
import {mapActions} from "vuex"
export default {
  data(){
    return {
      title:"Todo List",
      text:"",
      todos:[],
      isDone:false,
      id:0,
      editting:false,
      editText:""
    }
  },
  methods:{
    ...mapActions(["deleteTodo","editTodo"]),
    addTodo(){
      if(this.text.trim().length == 0){
        alert("please add todo")
      }
      else{
           this.todos.push({
        id:this.id,
        text:this.text,
        done:this.isDone
    }),
      this.text=""
      }
   
    },
    deleteTodo(id){
      console.log(id);
let del = this.todos.filter((e)=>{
  console.log(e.id);
  return e.id != id
}) 
   this.todos.pop(del)   },
   editTextChange(e){
    this.editText= e.target.value
   },
   editTodo(todo){
this.editting = this.editting == true ? false:true
if(this.editting){
  this.editText = todo.text
  let index = this.todos.findIndex((e)=>e.id == todo.id)

}
else{
  todo.text = this.editText
}

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

