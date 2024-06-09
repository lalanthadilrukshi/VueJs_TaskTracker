<template>
<div class="container">
 <Header @toggle-add-task='toggleAddTask' title="Task Tracker" :showAddTask="showAddTask"> </Header>
 <div v-if="showAddTask">
 <AddTask @add-task="addTask" />
</div>
 <Tasks @toggleReminder="toggleReminder" v-on:deleteTask="deleteTask"
 :tasks="tasks"/>
 </div>
</template>

<script >
import Header from "./components/Header.vue"
import Tasks from "./components/Tasks.vue"
import AddTask from "./components/AddTask.vue"

export default {
  name:"App",
  components:{
    Header,
    Tasks,
    AddTask,
  },
  data(){
    return{
      tasks:[],
      showAddTask:false,
    }      },

  methods:{
    toggleAddTask(){
    this.showAddTask= !this.showAddTask
    },
    async addTask(task) {
    const res=await fetch(`http://localhost:3000/tasks`,{
      method:"POST",
      headers:{
        "Content-type":"application/json"
      },
      body:JSON.stringify(task),
    })
    const data= await res.json()
    this.tasks=[...this.tasks,task]
    },
    async deleteTask(id){
    if (confirm("Are you shure you want to delete the task?")){
    const res = await fetch(`http://localhost:3000/tasks/${id}`, {method:'DELETE'})
   //if delete is successful the res will be 200
    res.status===200? (this.tasks=this.tasks.filter((task)=> task.id !==id) ) : alert ("error deleting")}
    alert(this.tasks)     },
    
  async toggleReminder(id){
  const taskToToggle =await this.fetchTasksById(id)
  const updTask = {...taskToToggle, reminder:!taskToToggle.reminder }
  const res = await fetch(`http://localhost:3000/tasks/${id}`, {
  method:'PUT',
  headers:{'Content-type':'application/json'},
  body:JSON.stringify(updTask),    })
  const data=await res.json()
  this.tasks =this.tasks.map((task)=>
  task.id=== id? {...task, reminder : !task.reminder} : task   )
  alert("toggle reminder - double click" + JSON.stringify(this.tasks) )  
  alert("data from res " + data)  }, 
  
  async fetchTasks(){
    const res=await fetch("http://localhost:3000/tasks")
    const data= await res.json()
    return data
  },
  async fetchTasksById(id){
    const res=await fetch(`http://localhost:3000/tasks/${id}`)
    const data= await res.json()
    return data
  },},
  
   async created(){
   this.tasks= await this.fetchTasks ()      },    }
</script>
<style scoped>
</style>
