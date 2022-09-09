<template>
  <v-dialog
    :value="true"
    width="600px">
    <v-card>
      <v-card-title>
        <span class="text-h5">Edit task</span>
      </v-card-title>
      <v-card-text>
        Edit the title of this task:

        <v-text-field
          v-model="taskTitle"
          @keyup.enter="saveTask">
        </v-text-field>

      </v-card-text>

      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn
          @click="$emit('close')"
          text>
          Cancel
        </v-btn>

        <v-btn
          @click="saveTask"
          :disabled="taskTitleInvalid"
          color="red darken-1"
          text>
          Save
        </v-btn>

      </v-card-actions>
    </v-card>
  </v-dialog>
</template>
<script>
export default {
  computed: {
    taskTitleInvalid() {
      return !this.taskTitle || this.taskTitle === this.task.title
    }
  },
  props: ['task'],
  data() {
    return {
      taskTitle: null
    }
  },
  methods: {
    saveTask() {
      if (!this.taskTitleInvalid) {
        let payload = {
          id: this.task.id,
          title: this.taskTitle
        }
        this.$store.dispatch('updateTaskTitle', payload)
        this.$emit('close')
        // this.$vuetify.goTo(0, { duration: 0 })
      }
    }

  },
  mounted() {
    this.taskTitle = this.task.title
  }
}
</script>
<style lang="">
    
</style>