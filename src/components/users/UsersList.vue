<template>
  <div class="users-list">
    <p v-if="isLoading">Loading...</p>
    <ul v-else-if="users.length">
      <users-item
          v-for="user in users"
          :key="user.id"
          :user="user"
      />
    </ul>
  </div>
</template>

<script>
import UsersItem from "@/components/users/UsersListItem.vue"
const FETCH_URL = "https://jsonplaceholder.typicode.com/users"
export default {
  name: "UsersList",
  components: {
    UsersItem,
  },
  data() {
    return {
      users: [],
      isLoading: false
    };
  },
  async mounted() {
    await this.fetchUsers()
  },
  methods: {
    async fetchUsers() {
      this.isLoading = true

      try {
        const res = await fetch(FETCH_URL)
        this.users = await res.json()
      } catch (error) {
        console.error("Error:", error)
      } finally {
        this.isLoading = false
      }
    }
  }
}
</script>

<style
  scoped
  lang="scss"
>
.users-list {
  padding: 0;
  margin: 0;

  ul {
    list-style: none;
    padding: 0;
  }
}
</style>