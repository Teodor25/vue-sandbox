<template>
    <header>
        <h1>{{title}}</h1>
        <Button :text="'Add task'" color="green" />
    </header>
</template>

<script>
import Button from './element-button.vue'

export default {
    name: 'layout-header',
    props: {
        title: String,
    },
    components: {
        Button
    }
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