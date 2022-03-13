<template>
    <header>
        <h1>{{title}}</h1>
        <Button :text="showAddTask ? 'Close' : 'Add task'" :color="showAddTask ? 'red' : 'green'" @click="$emit('toggle-add-task');"/>
    </header>
</template>

<script>
import Button from './element-button.vue'

export default {
    name: 'layout-header',
    props: {
        title: String,
        showAddTask: Boolean,
    },
    components: {
        Button,
    },
}
</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-content: center;
        margin-bottom: 20px;
    }
</style>