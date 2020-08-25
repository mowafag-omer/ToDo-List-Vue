<template>
  <span v-if="item.todo == false" class="done" @click="singleToggle(item.id)"><b-icon-check-circle-fill></b-icon-check-circle-fill> {{ item.name }}</span> 
  <span v-else  @click="singleToggle(item.id)"><b-icon-check2-circle></b-icon-check2-circle> {{ item.name }}</span> 
</template>

<script>
export default {
  name: 'singleTodo',
  props: {
    item: Object
  },
  methods: {
    singleToggle(id) {
      this.$emit('update', id)
    }
  }
}
</script>

<style scoped>
span{
  cursor: pointer;
}
.done{
  text-decoration: line-through;
  color: gray;
}
</style>