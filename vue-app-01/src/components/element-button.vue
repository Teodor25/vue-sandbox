<template>
    <button :style="{ background: color }" class="btn">{{text}}</button>
</template>

<script>
export default {
    name: "element-button",
    props: {
        text: {
            type: String,
            default: 'no text'
        },
        color: {
            type: String,
            default: "lightblue"
        }
    }
}
</script>

<style scoped>

</style>