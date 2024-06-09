<template>
    <form @submit="onSubmit" class="add-form" >
    <div class="form-control">
        <label>Tasks</label>
        <input type="text"  v-model="text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control" >
        <label>Day or time</label>
        <input type="text" v-model="day" name="day" placeholder="Add Day & Time" />
    </div>
    <div class="form-control form-control-check" >
        <label>Set Reminder</label>
        <input type="checkbox" v-model="reminder" name="reminder"  />
    </div>
    <input type="submit" value="Save Task"  class="btn btn-block" />       
    </form>
</template>

<script>
export default{
    name:"AddTask",
    data(){
        return{
            text:"test binding",
            day:"",
            reminder:false,
        }    },
    methods:{
        onSubmit(e) {
            e.preventDefault() // so that there is no actual submit
            if (!this.text){
                alert("please add a task")
                return
            }
            const newTask={
                //id: 5,
                text:this.text,
                day:this.day,
                reminder:this.reminder,
            } 
            this.$emit("add-task", newTask) 
           // alert (JSON.stringify(newTask))
        // clear the form
        this.text=""
        this.day=""
        this.reminder=false
        }     }        }
</script>

<style scoped>
.add-from{
    margin-bottom:4rem;
    display:block;}
.form-control {
margin:2rem 0;
width:100%;}
/*.form-control label{
    display:block;
}*/
.form-control input{
    width:100%;
    height:4rem;
    margin:.2rem;
    padding:.1rem .5rem;
    font-size:1.5rem;}
.form-control-check{
    display:flex;
   /* display:flex;
    justify-content:space-between;*/
    align-items:center;}
/*
.form-control-check label{
    flex:1;
} */
.form-control-check input{    
   /*flex:2;*/
    height:2rem;
    width:2rem;
    margin-left:auto;
    margin-right:0; }
    .btn{
        width : 100%;
    }
</style>