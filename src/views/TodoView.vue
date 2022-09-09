<template>
  <div class="home">

    <ListTasks
      v-if="$store.state.tasks.length">
    </ListTasks>

    <NoTasks
      v-else>
    </NoTasks>

    <ButtonDoneSorting
      v-if="$store.state.sorting">
    </ButtonDoneSorting>

  </div>
</template>

<script>

export default {
  name: 'Home',
  components: {
    'ListTasks': require('@/components/Todo/ListTasks.vue').default,
    'NoTasks': require('@/components/Todo/NoTasks.vue').default,
    'ButtonDoneSorting': require('@/components/Todo/ButtonDoneSorting.vue').default
  }
}
</script>
