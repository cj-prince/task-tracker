<template>
  <div class="container">
    <Header title='Task Tracker' />
    <Tasks  @delete-task="deleteTask" :tasks = 'tasks' />
  </div>
</template>

<script>
import Tasks from '@/components/Tasks.vue'
import Header from '@/components/Header.vue'
export default {
  name: 'App',
  components: {
   Header,
   Tasks,
  }, 
  data: () => ({
    tasks: [],
  }),
  methods:{
    deleteTask(id){
      this.tasks = this.tasks.filter((task) => task.id !== id)
    }
  },
  created(){
    this.tasks = [
      {
        id:1,
        text: 'Doctors Appointment',
        day: 'March Ist at 2:30pm',
        reminder: true
      },
      {
        id:2,
        text: 'Meeting at school',
        day: 'March 3rd at 12:30pm',
        reminder: true
      },
      {
        id:3,
        text: 'Going Home',
        day: 'March 6th at 15:30pm',
        reminder: false
      },
    ]
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
