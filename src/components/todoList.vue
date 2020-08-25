<template>
    <ul class="b-list-group">
      <li v-for="item in tdlist" :key="item.name">
        <singleTodo @update="todoToggle" :item='item'/>
      </li>
    </ul> 
</template>

<script>
import singleTodo from './singleTodo'

export default {
  name: 'todoList',
  components: {
    singleTodo
  },
  props: {
    tdlist: Array
  },
   methods: {
    todoToggle(id) {
      this.$emit('update-todo', id)
    }
  }
}
</script>

<style scoped>
li {
  list-style: none;
}
</style>