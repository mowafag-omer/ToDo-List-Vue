<template>
  <b-jumbotron>

    <template v-slot:header>Todo List</template>

    <template v-slot:lead>
      New Features we will have to done for this project
    </template>

    <hr class="my-3">

    <p>
      Easy to use, we created this web app just for you !
    </p>

    <sentence :listData="mydata"/>
    
    <hr class="my-3">
    
    <todoList @update-todo="jmbrToggle" :tdlist="mydata"/>

    <addForm @add="newTask"/>

  </b-jumbotron>
</template>

<script>
import todoList from './todoList'
import addForm from './addForm'
import sentence from './sentence'

export default {
  name: 'myJumbotron',
   components: {
    todoList,
    addForm,
    sentence
  },
  props: {
    mydata: Array
  },
   methods: {
    jmbrToggle(id) {
      this.$emit('update-elm', id)
    },
    newTask(task) {
      this.$emit('addnew', task)
    }
  }
}
</script>