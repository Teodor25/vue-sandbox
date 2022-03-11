<template>
    <div>
        <Task @delete-task="$emit('delete-task', task.id);" @toggle-reminder="$emit('toggle-reminder', task.id);" v-for="task in tasks" :task="task" :key="task.id"/>
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
    emits: ['delete-task', 'toggle-reminder']
}
</script>

<style scoped>

</style>