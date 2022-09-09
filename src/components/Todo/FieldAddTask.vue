<template>
    <v-text-field
        v-model="newTaskTitle"
        @keyup.enter="addTask"
        class="field-add-task pa-3"
        placeholder="Add task"
        hide-details
        clearable
        outlined>

        <template v-slot:append>
            <v-icon
                @click="addTask"
                :disabled="newTaskTitleInvalid">
                mdi-plus
            </v-icon>
        </template>

    </v-text-field>
</template>

<script>
export default {
    computed: {
        newTaskTitleInvalid() {
            return !this.newTaskTitle
        }
    },
    data() {
        return {
            newTaskTitle: '',
        }
    },
    methods: {
        addTask() {
            if (!this.newTaskTitleInvalid) {
                this.$store.dispatch('addTask', this.newTaskTitle)
                this.newTaskTitle = ''
            }
        },
    },
}
</script>

<style lang="sass">
// .field-add-task.v-input--is-focused {
//     & .v-input__control {
//         background: #205e7f !important
//     }
// }

.field-add-task.v-input--is-focused .v-input__control 
        background: RGBA(32, 94, 127, .4) !important
</style>
