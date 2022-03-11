<template>
    <button 
        :style="{ background: color }" 
        class="btn" 
        @click="onClick()"
    >
        {{text}}
    </button>
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
    },
    methods: {
        onClick() {
            alert('Click');
        }
    }
}
</script>

<style scoped>

</style>