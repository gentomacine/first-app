<template>
  <div class="container">
<Header @toggle-add-task="toggleAddTask"
 title="Task Tracker"
 :showAddTask="showAddTask"/>
<div v-if="showAddTask">
<AddTask @add-task="addTask" />
</div >
<Tasks @toggle-reminder="toggleReminder" 
 @delete-task="deleteTask" :tasks="tasks"/>
  </div>
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'
export default {
  name: 'App',
  components: {
  Header,
  Tasks,
  AddTask,

  
  },
  data(){
    return{
      tasks:[],
      showAddTask: true
    }
    
    //if vue instance is created,
  
  //created() hook allows you to add code to be run

  },
  methods:{
    toggleAddTask(){
      this.showAddTask=!this.showAddTask

    },
    addTask(task){
      this.tasks = [this.tasks, task]
    },

    deleteTask(id){
      if(confirm('Are you sure?')){
        this.tasks=this.tasks.filter((task)=> 
      task.id !== id)

      }
      
    },

    
    
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) => 
       task.id === id ? { ...task, reminder: !task.reminder
      } : task
    )
    },
    async fetchTasks(){
      const res = await fetch('http://localhost:5000/tasks')
      const data = await res.json()
      return data
    }
  },
  created(){
    this.tasks=[
      {
        id:1,
        text:"Doctors Appointment",
        day: "march 1st at 10:30am",
        reminder: true,
      },
      {
        id:2,
        text:"fellowship",
        day: "August 1st at 6:00pm",
        reminder: true,
      },
      {
        id:3,
        text:"Food Shoppig",
        day: "sept 1st at 2:30pm",
        reminder: false,
      },
      {
        id:4,
        text:"wedding",
        day: "June 1st at 12:30pm",
        reminder: true,
        },
        
    ]
  }

}

</script>

<style>
*{
  box-sizing:border-box;
  margin:0;
  padding:0;
}
body{
  font-family: 'poppins',Arial, Helvetica, sans-serif;
  

}

.container{
  max-width: 800px;
  margin: 30px auto;
  overflow: auto;
  min-height:500px;
  border:1px solid steelblue;
  padding:30px;
  border-radius:5px;
  background-color: rgb(117, 121, 120);
}
.btn{
  display:inline-block;
  background:rgb(179, 164, 164);
  color:#fff;
  border:none;
  padding:10px 20px;
  margin:5px;
  border-radius:5px;
  cursor:pointer;
  text-decoration:none;
  font-size:15px;
  font-family:inherit;


}
.btn:focus{
  outline:none;
}
.btn:active{
  transform:scale(0.98)
}
.btn-block{
  display:block;
  width:100%;
}
</style>
