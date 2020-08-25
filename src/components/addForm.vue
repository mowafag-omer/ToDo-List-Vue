<template>
  <b-form action='/'>
    <b-input-group prepend="New Task" class="mb-2 mx-auto w-50">
      <b-input id="inline-form-input-username" v-model="task" placeholder="Todo Name"></b-input>
      <b-button @click="addTaskForm" variant="secondary"><b-icon-file-plus></b-icon-file-plus> Add</b-button>
    </b-input-group>
  </b-form>
</template>

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

<style scoped>

</style>