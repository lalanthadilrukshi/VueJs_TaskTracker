<template>
 <div 
    @dblclick="$emit('toggleReminder', task.id)"
    :class="[task.reminder ? 'reminder' : '' , 'task']" >
    <h3>{{task.text}}
    <i v-on:click="onDelete(task.id)" class="fas fa-times"></i>
    </h3>
    <p>{{ task.day }}</p>
</div>
</template>

<script>
export default {
    name:'Task',
    props:{
        task:Object,
    },
    methods:{
        onDelete(id){
            console.log("id clicked " + id)
            this.$emit("deleteTask", id)
        },
    },

    emits:["toggleReminder", "deleteTask"]
}
</script>
<style>
.task{
    background:#f4f4f4;
    margin:.5rem;
    padding: 1rem 2rem;
    cursor:pointer;
}

.task.reminder{
    border-left: .5rem solid green;
}
.task h3{
    display:flex;
    align-items:center;
    justify-content:space-between;
}
.fas{
    color:red;
}
</style>