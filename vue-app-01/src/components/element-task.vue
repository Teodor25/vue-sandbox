<template>
    <div class="task" :class="classObject" @dblclick="$emit('toggle-reminder', task.id)">
        <h3>{{task.text}}
            <i class="fas fa-times" @click="$emit('delete-task', task.id);"></i>
        </h3>
        <p>{{task.day}}</p>
    </div>
</template>

<script>
export default {
    name: 'element-task',
    props: {
        task: Object
    },
    computed: {
        classObject: function() {
                return {
                    reminder: this.task.reminder,
                    'deadline': this.task.deadline
                }
            }
    },
    emits: ['delete-task', 'toggle-reminder']
}
</script>

<style scoped>
.fas:hover {
    transform: scale(1.1);
    color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task.deadline {
    background: rgb(255, 236, 236);
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>