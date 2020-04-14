<template>
  <div class="todo-item" v-bind:class="{'is-complete':todoItem.completed}">
    <!-- <p>{{todoItem.id}}</p> -->
    <p>
      <input type="checkbox" v-on:change="markComplete">
      {{todoItem.title}}
      <button v-on:click="$emit('del-todoItem', todoItem.id)" class="del">x</button>
    </p>    
    <!-- <p>{{todoItem.completed}}</p> -->
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todoItem"],
  methods: {
    markComplete() {
      this.todoItem.completed = !this.todoItem.completed;      
    }
  }
}
</script>

<style scoped>
  .todo-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
  }

  .is-complete {
    text-decoration: line-through;
  }

  .del {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
  }
</style>