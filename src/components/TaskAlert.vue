<template>
  <div class="alert alert-warning d-flex justify-content-between align-item-center">
    <p :class="{'tachado': task.state}">{{ task.name }}</p>
    <div>
      <i class="fas fa-undo-alt mx-2 text-primary" role="button" title="check"
        @click="editTask(task.id)"
        v-if="task.state"
      ></i>
      <i class="fas fa-check-circle mx-2 text-success" role="button" title="check"
        @click="editTask(task.id)"
        v-else
      ></i>
      <i class="fas fa-minus-circle text-danger" role="button" title="delete"
        @click="deleteTask(task.id)"
      ></i>
    </div>
  </div>
</template>

<script>
import { inject } from 'vue'
export default {
  props: {
    task: {
      type: Object,
      required: true
    }
  },
  setup() {
    const tasks = inject('tasks')

    const deleteTask = id => {
      tasks.value = tasks.value.filter(task => task.id !== id)
    }

    const editTask = id => {
      tasks.value = tasks.value.map(item => {
          if(item.id === id) {
            item.state = !item.state
          }
          return item
      })
    }
    return { deleteTask, editTask }
  }

}
</script>

<style>
  .tachado {
    text-decoration: line-through;
  }
</style>