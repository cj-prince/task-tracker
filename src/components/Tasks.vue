<template>
  <div v-for="task in tasks" :key="task.id">
    <div  @dblclick="$emit('toggle-reminder', task.id)" :class="['task', task.reminder ? 'reminder' : '']" >
      <h3>{{task.text}} <i @click="onDelete(task.id)" class="fas fa-times"></i></h3>
      <p>{{task.day}}</p>
    </div>
  </div>
</template>

<script>
// import Task from './Task.vue'
  export default {
    name: 'Task',
    props: {
      tasks: Array
    },
    components: {
      // Task,
    },
    methods:{
      onDelete(id){
        this.$emit('delete-task', id)
      }
    },
    emits:['delete-task','toggle-reminder']
  }
</script>

<style scoped>
  .fas {
    color: red;
  }
  .task {
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
  }
  .task.reminder {
    border-left: 5px solid green;
  }
  .task h3 {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
</style>