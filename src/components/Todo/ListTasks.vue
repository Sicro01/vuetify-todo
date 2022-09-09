<template>
  <v-list
    class="pt-0"
    flat>
    <draggable
      v-model="tasks"
      handle=".handle">
      <Task
        v-for="task in tasks"
        :key="task.id"
        :task="task">
      </Task>
    </draggable>

  </v-list>
</template>

<script>
import draggable from 'vuedraggable'

export default {
  computed: {
    tasks: {
      get() {
        return this.$store.getters.tasksFiltered
      },
      set(value) {
        this.$store.dispatch('setTasks', value)
      }
    }
  },
  components: {
    draggable,
    'Task': require('@/components/Todo/Task.vue').default
  }
}
</script>
