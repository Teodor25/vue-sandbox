<template>
    <div>
        <Task @delete-task="$emit('delete-task', task.id);" v-for="task in tasks" :task="task" :key="task.id"/>
    </div>
</template>

<script>
import Task from './element-task.vue';

export default {
    name:'element-task-list',
    props: {
        tasks: Array
    }, 
    components: {
        Task
    },
    emits: ['delete-task']
}
</script>

<style scoped>

</style>