<template>
  <div>
    <div v-bind:key="items.id" v-for="items in todos">
      <TodoItem v-bind:todoItem="items" v-on:del-todoItem="$emit('del-todoItem', items.id)" />
    </div>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue'

export default {
  name: "Todos",
  components: {
    TodoItem
  },
  props: ["todos"]
}
</script>

<style scoped>

</style>