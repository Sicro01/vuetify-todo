<template>
    <div>
        <v-list-item
            @click="$store.dispatch('doneTask', task.id)"
            :class="{ 'blue lighten-5': task.done }"
            class="white"
            :ripple="false">
            <template v-slot:default>

                <v-list-item-action>
                    <v-checkbox :input-value="task.done"></v-checkbox>
                </v-list-item-action>

                <v-list-item-content>
                    <v-list-item-title
                        :class="{ 'text-decoration-line-through': task.done }">
                        {{ task.title }}
                    </v-list-item-title>
                </v-list-item-content>

                <v-list-item-action v-if="task.dueDate">
                    <v-list-item-action-text>
                        <v-icon small>mdi-calendar</v-icon>
                        {{ task.dueDate | niceDate }}
                    </v-list-item-action-text>
                </v-list-item-action>

                <v-list-item-action>
                    <TaskMenu :task="task"></TaskMenu>
                </v-list-item-action>

                <v-list-item-action
                    v-if="$store.state.sorting">
                    <v-btn
                        class="handle"
                        color="primary"
                        icon>
                        <v-icon>mdi-drag-horizontal-variant</v-icon>
                    </v-btn>
                </v-list-item-action>

            </template>

        </v-list-item>

        <v-divider></v-divider>

    </div>
</template>

<script>
import { format } from 'date-fns'

export default {
    props: ['task'],
    filters: {
        niceDate(value) {
            return format(new Date(value), 'MMM d')
        }
    },
    components: {
        "TaskMenu": require("@/components/Todo/TaskMenu.vue").default
    }
}
</script>

<style lang="sass">
    .sortable-chosen
        box-shadow: 0 0 10px rgba(0,0,0,0.3)
</style>
