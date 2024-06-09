<template>
    <div :key="task.id" v-for="task in tasks">
    <Task @toggleReminder="$emit('toggleReminder',task.id)"
    v-on:deleteTask="$emit('deleteTask',task.id)" :task="task" />
    </div>
</template>

<script>
import Task from "./Task.vue"
export default {
    name:"Tasks",
    props:{
        tasks: Array,
    },
    components:{
        Task
    },
    emits:["deleteTask","toggleReminder"],
}
</script>