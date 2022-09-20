<template>
  <div class="container">
    <Header title='Task Tracker' @toggle-addTask='toggleAddTask' :showAddTask='showAddTask' />
    <div v-show="showAddTask">
      <AddTask  @add-task ='addTask'/>
    </div>
    
    <Tasks @toggle-reminder='toggleReminder' @delete-task="deleteTask" :tasks = 'tasks' />
  </div>
</template>

<script>
import Tasks from '@/components/Tasks.vue'
import Header from '@/components/Header.vue'
import AddTask from '@/components/AddTask.vue'
export default {
  name: 'App',
  components: {
   Header,
   Tasks,
   AddTask,
  }, 
  data: () => ({
    tasks: [],
    showAddTask: false
  }),
  methods:{
    async deleteTask(id){
      const response =  await fetch(`api/tasks/${id}`, {
        method: 'DELETE'
      })
      response.status === 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id)) : alert('request failed')
      
    },
    async toggleReminder(id){
      const taskToggle =  await this.fetchTask(id)
      const updateTask = {...taskToggle, reminder: !taskToggle.reminder}
      const response = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'content-type':'application/json'
        },
        body: JSON.stringify(updateTask)
      })
      const data = await response.json()
      this.tasks = this.tasks.map((task) => task.id ===id ? {...task, reminder: data.reminder}: task)
    },
    async addTask(task){
      const response = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'content-type': 'application/json',
        },
        body: JSON.stringify(task)
      })

      const data = await response.json()
      this.tasks = [...this.tasks, data]
    },
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    }, 
    async fetchTasks(){
      const response = await fetch('api/tasks')

      const data = response.json() //fetching data from json server
      return data
    },
    async fetchTask(id){
      const response = await fetch(`api/tasks/${id}`)

      const data = response.json() //fetching single task data from json server
      return data
    },
  },
  async created(){
    this.tasks = await this.fetchTasks()
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
