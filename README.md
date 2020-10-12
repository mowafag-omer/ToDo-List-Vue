# todo-list
![](https://img.shields.io/badge/vue.js-gray?logo=vue.js)
![](https://img.shields.io/badge/Bootstrap_vue-gray?logo=Bootstrap)

todo-list project using Vue.js without a server-side

<br>
<img src="https://github.com/mowafag-omer/ToDo-List-Vue/blob/master/Capture.PNG" width="80%" height="80%">

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```
<br>

## Code

### App.vue

the principal component which contains myJumbotron component which contains all the components and the data for the app. 
there are two methods; taggole to change task status and addNewTask to add new task.

- template
```
<template>
  <div id="app">
    <myJumbotron @update-elm="toggle" @addnew="addNewTask" v-bind:mydata="list"/>
  </div>
</template>
```
- script
```
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
```
<br>

### myJumbotron.vue

myJumbotron component which contains (todoList, addForm, sentence). 
there are two methods; <b>jmbrToggle</b> method which emits "update-elm" event to change task status in App component and <b>newTask</b> which emits "newTask" event to add new task in App component. Passing the data recived from App component to todoLidt component as props

- template
```
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
```

- script
```
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
      this.$emits('update-elm', id)
    },
    newTask(task) {
      this.$emits('addnew', task)
    }
  }
}
</script>
```
<br>

### todoList.vue

todoList component which contain sigleTodo. 
<b>todoToggle</b> emits "update-todo" event to the parent component to change task status.
loop through the tasks array recived form myJumbotron component in the sigleTodo and set each task as props

- template
```
<template>
    <ul class="b-list-group">
      <li v-for="item in tdlist" :key="item.name">
        <singleTodo @update="todoToggle" :item='item'/>
      </li>
    </ul> 
</template>
```

- script
```
script>
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
      this.$emits('update-todo', id)
    }
  }
}
</script>
```

<br>

### todoList.vue

Showing each task individually. 
<b>singleToggle</b> emits "update-todo" event to the parent component (todoList) to change task status.

- template
```
<template>
  <span v-if="item.todo == false" class="done" @click="singleToggle(item.id)"><b-icon-check-circle-fill></b-icon-check-circle-fill> {{ item.name }}</span> 
  <span v-else  @click="singleToggle(item.id)"><b-icon-check2-circle></b-icon-check2-circle> {{ item.name }}</span> 
</template>
```

- script
```
<script>
export default {
  name: 'singleTodo',
  props: {
    item: Object
  },
  methods: {
    singleToggle(id) {
      this.$emits('update', id)
    }
  }
}
</script>
```

<br>

### addForm.vue

addForm contains the form and It emits "add" event and sent  to the parent component (myJumbotron).

- template
```
<template>
  <b-form action='/'>
    <b-input-group prepend="New Task" class="mb-2 mx-auto w-50">
      <b-input id="inline-form-input-username" v-model="task" placeholder="Todo Name"></b-input>
      <b-button @click="addTaskForm" variant="secondary"><b-icon-file-plus></b-icon-file-plus> Add</b-button>
    </b-input-group>
  </b-form>
</template>
```

- script
```
<script>
export default {
  name: 'addForm',
  data() {
    return {
      task: ''
    }
  },
  methods: {
    addTaskForm() {
      this.$emit('add', this.task)
      this.task = ''
    }
  }
}
</script>
```
