<template>
  <li class="users-list-item">
    <h3 class="item-title">{{ user.name }}</h3>

    <div
      v-if="showDetails"
      class="item-details"
    >
      <p>Email: {{ user.email }}</p>
      <p>Phone: {{ user.phone }}</p>
    </div>

    <div
        class="item-toggle-detail"
        @click="toggleDetails"
    >
      {{ showDetails ? "Hide Details" : "Show Details" }}
    </div>
  </li>
</template>

<script>
export default {
  name: "UsersListItem",
  props: {
    user: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      showDetails: false,
    }
  },
  methods: {
    toggleDetails() {
      this.showDetails = !this.showDetails
    }
  }
}
</script>

<style
  scoped
  lang="scss"
>
@use "@/style/media.mixins" as *;

.users-list-item {
  position: relative;
  padding: 20px 10px;


  &:not(:last-of-type) {
    border-bottom: 1px solid #999;
  }

  @include phone-down {
    min-width: 500px;
  }

  .item-details {
    margin-top: 5px;
  }

  .item-toggle-detail {
    position: absolute;
    top: 20px;
    right: 20px;
    cursor: pointer;
  }
}
</style>