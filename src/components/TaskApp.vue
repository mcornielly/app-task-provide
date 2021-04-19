<template>
    <h1>App Tareas</h1>
    <task-form />
    <hr>
    <task-alert v-for="task in tasks" :key="task.id" :task="task" />
    <div class="alert alert-dark mt-3" v-if="tasks.length === 0">
        Sin Tareas Pendientes 😊
    </div>
    <p>
        {{ tasks }}
    </p>
</template>

<script>
import { provide, ref, watchEffect } from 'vue'
import TaskForm from './TaskForm'
import TaskAlert from './TaskAlert'
export default {
    components: {
        TaskForm,
        TaskAlert
    },
    setup() {
        const tasks = ref([])

        provide('tasks', tasks)

        if(localStorage.getItem('tasks')) {
            tasks.value = JSON.parse(localStorage.getItem('tasks'))
        }

        watchEffect(() => {
            localStorage.setItem('tasks', JSON.stringify(tasks.value))
        }) 
        

        return { tasks }
    }
}
</script>

<style>

</style>