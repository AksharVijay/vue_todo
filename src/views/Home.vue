<template>
  <div id="app">
      <AddTodo v-on:add-todo="addTodo"/>
      <Todos v-bind:todos="todosData" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import AddTodo from '../components/AddTodo';
import Todos from '../components/Todos';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },
  data () {
    return {
      todosData : [
        // {
        //   id : 1,
        //   title : 'Todo One',
        //   completed : false
        // },
        // {
        //   id : 2,
        //   title : 'Todo Two',
        //   completed : true
        // },
        // {
        //   id : 3,
        //   title : 'Todo Three',
        //   completed : false
        // }
      ]
    }
  },
  methods : {
    deleteTodo (id) {
       this.todosData = this.todosData.filter( todo => todo.id !== id );
    },
    addTodo(newTodo) {
      this.todosData = [...this.todosData, newTodo];
    }
  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
    .then(res=> this.todosData = res.data)
    .catch(err => console.log(err));
  }
}
</script>

<style>
*{
  margin : 0px;
  padding: 0px;
  box-sizing: border-box;
}

body {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  line-height: 1.4;
}

.btn{
  display: inline-block;
  border: none;
  background: #555;
  color:#fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
