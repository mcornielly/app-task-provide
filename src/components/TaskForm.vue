<template>
    <form @submit.prevent="addTask">
        <input 
            type="text"
            class="form-control my-2"
            placeholder="Ingrese Tarea"
            v-model.trim="text"
        >
        <button type="submit" class="btn btn-primary w-100">Agregar</button>
    </form>
</template>

<script>
import { inject, ref } from 'vue'

export default {
    setup() {
        const text = ref('')
        const tasks = inject('tasks')

        const addTask = () => {
            if(text.value === ''){
                return console.log('Vacio')
            }
            const task = {
                id: Date.now(),
                name: text.value,
                state: false
            }
            console.log(task)
            tasks.value.push(task)
            text.value = ''
        }

        return { addTask, text }
    }
}
</script>
