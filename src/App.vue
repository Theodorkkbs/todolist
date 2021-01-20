<template>
<div class="jumbotron jumbotron-fluid text-light">
  <div class="container">
    <h1 class="display-4">Todo List</h1>
    <p class="lead">Manage day-to-day tasks</p>
  </div>
</div>
<br>
<br>
<div class="container">
  <div class="row">
    <div class="col-md-4 offset-4">
      <input type="text" id="taskip" @keydown.enter="insertItem" v-model="inputTerm" placeholder="Add Task Here">
    </div>
  </div>
  <br>
  <br>
  <div class="row">
    <div class="col-md-12">
      <h3 style="text-align:center">Task List</h3>
      <table class="table table-striped">
  <thead class="thead-dark">
    <tr>
      <th scope="col">ID</th>
      <th scope="col">Name</th>
      <th scope="col">Mark completed</th>
      <th scope="col">Remove task</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task,index) in todolist" v-bind:key="task">
      <td>{{task.id}}</td>
      <div v-if="!task.editing">
      <td v-on:dblclick="editTask(task)" v-bind:class="{completed:task.isCompleted}">{{task.name}}</td>
      </div>
         <input v-else  @blur="editCompleted(task)" @keydown.enter="editCompleted(task)" v-model="task.name" type="text">
      <td><input type="checkbox" v-model="task.isCompleted"></td>
      <td><button @click="deleteTask(index)" class="btn btn-sm bg-danger">Remove</button></td>
    </tr>
  </tbody>
    </table>
    </div>
  </div>
</div>
</template>

<script>

export default {

data(){
  return{
    inputTerm:'',
    id:0,
    todolist:[],
  }
},

methods:{

insertItem(){

this.todolist.push({name:this.inputTerm,isCompleted:false,id:this.id,editing:false})
this.inputTerm=''
this.id+=1
console.log(this.todolist)

},

editTask(task){
  task.editing=true
},

editCompleted(task){
  task.editing=false

},

deleteTask(index){
  this.todolist.splice(index,1)
}

}

}


</script>


<style>
  @import './assets/style.css';


</style>