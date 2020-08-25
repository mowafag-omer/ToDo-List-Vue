<template>
  <div id="app">
    <myJumbotron @update-elm="toggle" @addnew="addNewTask" v-bind:mydata="list"/>
  </div>
</template>

<script>
import myJumbotron from './components/myJumbotron'

export default {
  name: 'App',
  components: {
    myJumbotron
  },
  data() {
    return {
      list: [
        {id: 0, name: "Ecrire le sujet", todo: true},
        {id: 1, name: "Faire le sujet", todo: true},
        {id: 2, name: "Vendre le sujet", todo: true},
        {id: 3, name: "Partir en vaccances", todo: true}
      ]
    }
  },
  methods: {
    toggle(id) {
      this.list.forEach(element => {
        if(element.id === id && element.todo == true){
          element.todo = false
        } else if(element.id === id && element.todo == false) {
          element.todo = true
        }
      })
    },
    addNewTask(task){
      const newTask = {
        id: (this.list.length) + 1,
        name: task,
        todo: true
      }
      this.list.push(newTask)
    }
  }
} 
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>