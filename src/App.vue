<template>
  <base-layout>
    <users-list />
  </base-layout>
</template>

<script>
import BaseLayout from "@/views/BaseLayout.vue"
import UsersList from "@/components/users/UsersList.vue"

export default {
  name: 'App',
  components: {
    BaseLayout,
    UsersList
  }
}
</script>
