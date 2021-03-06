<template>
  <div id="app">
    <table>
      <tbody>
        <tr id="TableHead">
          <th> <button @click="addToDo()" >New Deal</button> </th>
          <th> <button @click="ChangeEdit" :class="[edit ? 'activeButton': '']">Edit</button> </th>
        </tr>
      </tbody>
    </table>
    <ToDoList :todos="todos" :edit="edit"   
    @done-todo="doneToDo" @delete-todo="deleteToDo" 
    @add-todo="addToDo" @redact-todo="redactToDo"/>
  </div>
</template>

<script>
import ToDoList from './components/ToDoList.vue'

export default {
  name: 'App',
  data(){
    return{
      todos: [
        { id: 1, name: 'Deal', isActive: true },
        { id: 2, name: 'Done', isActive: true }, 
        { id: 3, name: 'Loll', isActive: true },
      ],
      edit: false,
    }
  },
  components: {
    ToDoList
  },
  methods: {
    deleteToDo(index){
     this.todos.splice(index, 1); 
    },
    doneToDo(index){
      this.todos[index].isActive = !this.todos[index].isActive;
    },
    addToDo(){
      let newDeal = prompt('Enter the name of the case');
      if (newDeal){
        this.todos.unshift({ id: this.todos.length + 2, name: newDeal, isActive: true },)
      }
    },
    redactToDo( index, changeDeal){
      this.todos[index].name = changeDeal;
    }, 
    ChangeEdit(){
      this.edit = !this.edit;
    }
  }
}
</script>
<style>
  *{
    margin: 0;
    padding: 0;
    font-family: 'Poppins', sans-serif;
  }
  ::-webkit-scrollbar {
  width: 0;
  }
  #app {
    background: rgb(66,1,255);
    background: linear-gradient(90deg, rgba(66,1,255,1) 0%, rgba(212,0,152,1) 82%, rgba(236,0,69,1) 100%);
    height: 100vh;
  }
  #TableHead{
    display: flex;
    justify-content: space-between;
    height: 50px;
    width: calc(100vw - 3px);
  }
  #TableHead th{
    display: flex;
  }
  button{
    background-color: #ffffff00;
    border: 2px solid rgb(0, 0, 0);
    width: 150px;
    font-size: 20px;
  }
  button:hover{
    background-color: rgb(0, 0, 0);
    color: #ffffff;
    transition: 0.3s ease-in-out;
  }
  .activeButton{
    background-color: rgb(0, 0, 0);
    color: #ffffff;
  }
</style>
