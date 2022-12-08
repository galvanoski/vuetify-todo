<template>
  <div class="home pa-0">



    <list-tasks v-if="$store.state.tasks.length"></list-tasks>

    <no-tasks v-else></no-tasks>

    <button-done-sorting
     v-if="$store.state.sorting"
     ></button-done-sorting>
  </div>

</template>

<script>

export default {
  name: 'Home',

  components: {
    'list-tasks': require('@/components/todo/ListTasks.vue').
      default,
    'no-tasks': require('@/components/todo/NoTasks.vue').
      default,
    'button-done-sorting': require('@/components/todo/ButtonDoneSorting.vue').
      default
  }

}
</script>
