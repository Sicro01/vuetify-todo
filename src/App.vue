<template>
  <v-app
    id="inspire">
    <v-navigation-drawer v-model="drawer" app :mobile-breakpoint="768">
      <v-img
        class="pa-4 pt-7"
        gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
        height="170"
        src="mountains.jpg">
        <v-avatar
          class="mb-2"
          size="62">
          <img src="simon.jpg" alt="Simon">
        </v-avatar>
        <div class="white--text text-subtitle-1 font-weight-bold">
          Simon Cropper
        </div>
        <div class="white--text text-subtitle-2">
          simon_cropper
        </div>
      </v-img>

      <v-list dense nav>
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.to"
          link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      color="primary"
      height="170"
      src="mountains.jpg"
      app
      dark
      :height="$route.path === '/' ? '238' : '170'"
      prominent>
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.9), rgba(128,208,199,.9)">
        </v-img>
      </template>

      <v-container class="header-container pa-0">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <Search></Search>
        </v-row>

        <v-row>
          <v-app-bar-title class="text-h4 ml-4">
            {{ $store.state.appTitle }}
          </v-app-bar-title>
        </v-row>

        <v-row>
          <LiveDateTime></LiveDateTime>
        </v-row>
        <v-row v-if="$route.path === '/'">
          <FieldAddTask></FieldAddTask>
        </v-row>

      </v-container>

    </v-app-bar>

    <v-main>
      <router-view></router-view>
      <SnackBar></SnackBar>
    </v-main>
  </v-app>
</template>

<script>
export default {
  mounted() {
    this.$store.dispatch('getTasks')
  },
  data: () => ({
    drawer: null,
    items: [
      { title: "Todo", icon: "mdi-format-list-checks", to: "/" },
      { title: "About", icon: "mdi-help-box", to: "/about" },
    ],
  }),
  components: {
    'FieldAddTask': require('@/components/Todo/FieldAddTask.vue').default,
    "LiveDateTime": require("@/components/Tools/LiveDateTime.vue").default,
    "Search": require("@/components/Tools/Search.vue").default,
    "SnackBar": require("@/components/Shared/SnackBar.vue").default,
  },
};
</script>
<style lang="sass">
 .header-container
     max-width: none !important

</style>