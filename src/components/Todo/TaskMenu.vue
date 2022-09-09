<template>
  <div>
    <v-menu bottom
      left>
      <template v-slot:activator="{ on, attrs }">
        <v-btn v-bind="attrs"
          v-on="on"
          color="primary"
          icon>
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>
      </template>

      <v-list>
        <v-list-item v-for="(item, index) in items"
          :key="index"
          @click="handleClick(index)">
          <v-list-item-icon>
            <v-icon v-text="item.icon"></v-icon>
          </v-list-item-icon>

          <v-list-item-title>{{ item.title }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>

    <DialogDelete v-if="dialogs.delete"
      @close="dialogs.delete = false"
      :task="task">
    </DialogDelete>

    <DialogEdit v-if="dialogs.edit"
      @close="dialogs.edit = false"
      :task="task">
    </DialogEdit>

    <DialogDueDate v-if="dialogs.dueDate"
      @close="dialogs.dueDate = false"
      :task="task">
    </DialogDueDate>
  </div>
</template>
<script>
export default {
  props: ["task"],
  data: () => ({
    dialogs: {
      edit: false,
      delete: false,
      dueDate: false,
    },
    items: [
      {
        title: "Edit",
        icon: "mdi-pencil",
        click() {
          this.dialogs.edit = true;
          console.log("edit");
        },
      },
      {
        title: "Due Date",
        icon: "mdi-calendar",
        click() {
          this.dialogs.dueDate = true;
          console.log("due date");
        },
      },
      {
        title: "Delete",
        icon: "mdi-delete",
        click() {
          this.dialogs.delete = true;
          console.log("delete");
        },
      },
      {
        title: "Sort",
        icon: "mdi-drag-horizontal-variant",
        click() {
          if (!this.$store.state.search) {
            this.$store.commit('toggleSorting')
          }
          else {
            this.$store.commit('showSnackbar', 'How dare you try to sort while searching!')
          }
        },
      },
    ],
  }),
  methods: {
    handleClick(index) {
      this.items[index].click.call(this);
    },
  },
  components: {
    DialogEdit: require("@/components/Todo/Dialogs/DialogEdit.vue").default,
    DialogDelete: require("@/components/Todo/Dialogs/DialogDelete.vue").default,
    DialogDueDate: require("@/components/Todo/Dialogs/DialogDueDate.vue")
      .default,
  },
};
</script>
<style lang=""></style>
