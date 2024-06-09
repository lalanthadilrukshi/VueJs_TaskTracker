<template>
<header> 
<h1>{{ title }}  </h1>
<Button @vButtonClick = "$emit('toggle-add-task')"  :text="showAddTask? 'close' : 'Add Task'" color="green" > </Button>
</header>
</template>

<script>
import Button from "./Button.vue"

export default{
    name:"Header",
   
props:{
title:String,
showAddTask:Boolean,
},
components:{
    Button,
},

}
</script> 

<style>
@import url('https://fonts.googleapis.com/css2?family=Briem+Hand:wght@100..900&display=swap');
*{
    box-sizing: border-box;
    margin:0;
    padding:0;
}
body{
    font-family:"Briem Hand" , sans-serif;
}
.container{
    max-width:50rem;
    margin:3rem auto;
    overflow:auto;
    min-height: 30rem;
    border: 0.2rem solid steelblue;
    padding:3rem;
    border-radius:.5rem;
}
.btn{
    display: inline-block;
    background:black;
    color:white;
    border:none;
    padding: 1rem 2rem;
    margin:.5rem;
    border-radius: .5rem;
    cursor:pointer;
    text-decoration: none;
    font-size: 1.5rem;
    font-family: inherit;
}
header{
    display:flex;
    justify-content:space-between;
    align-items:center;
    margin-bottom:20px;}
</style>