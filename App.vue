<template>
  <div id="app">
    <Header />
    <AddTodoItem v-on:add-todo="addTodoItem"/>
    <Todos v-bind:todos="todosList" v-on:del-todoItem="deleteTodoItem" />
  </div>
</template>

<script>
import Header from './components/layout/Header';
import Todos from './components/Todos';
import AddTodoItem from './components/AddTodoItem';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Header,
    Todos,
    AddTodoItem
  },
  data() {
    return {
      todosList: []
    }
  },
  methods: {
    deleteTodoItem(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res => { 
        this.todosList = this.todosList.filter(todosList => todosList.id !== id);
        return res;
        })
      .catch(err => console.log(err));      
    },
    addTodoItem(newTodo) {
      const { title, completed} = newTodo;

      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
        .then(res => this.todosList = [...this.todosList, res.data])
        .catch(err => console.log(err));      
    }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(res => this.todosList = res.data)
    .catch(err => console.log(err));
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }

  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover {
    background: #666;
  }
</style>
