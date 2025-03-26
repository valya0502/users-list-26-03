<template>
  <div class="base-layout">
    <base-header />

    <main class="base-layout__container">
      <div class="content">
        <div class="content-wrapper">
          <slot />
        </div>
      </div>

      <transition name="sidebar-transition">
        <div class="sidebar" v-if="!isSidebarHidden">
          <base-sidebar class="sidebar-wrapper"/>
        </div>
      </transition>

    </main>

    <base-footer />
  </div>
</template>

<script>
import BaseHeader from "@/components/layout/BaseHeader.vue"
import BaseSidebar from "@/components/layout/BaseSidebar.vue"
import BaseFooter from "@/components/layout/BaseFooter.vue"
import UsersList from "@/components/users/UsersList.vue"
const TABLET_MAX_WIDTH = 700
export default {
  name: 'BaseLayout',
  components: {
    BaseHeader,
    BaseSidebar,
    BaseFooter,
    UsersList
  },
  data() {
    return {
      isSidebarHidden: false,
      windowWidth: null
    }
  },
  mounted() {
    window.addEventListener('resize', this.handleResize)
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.handleResize)
  },
  methods: {
    handleResize() {
      this.windowWidth = window.innerWidth || document.documentElement.clientWidth || document.body.clientWidth
      this.isSidebarHidden = this.windowWidth <= TABLET_MAX_WIDTH
    }
  }
}
</script>

<style
  scoped
  lang="scss"
>
@use "@/style/media.mixins" as *;
$sidebar-width: 300px;

.base-layout {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  min-height: 100vh;

  .base-layout__container {
    display: grid;
    grid-template-columns: minmax(0, 1fr) $sidebar-width;
    flex-grow: 1;
    overflow: hidden;
    position: relative;
    transition: all 250ms ease-in-out;

    @include tablet-down {
      grid-template-columns: minmax(0, 1fr) 0;
    }
  }
}

.content {
  width: 100%;
  flex-grow: 1;

  .content-wrapper {
    height: 100%;
    width: 100%;
    max-width: 800px;
    min-width: 500px;
    padding: 10px;
    margin: 0 auto;
    background: #fff;

    @include tablet-large-down {
      min-width: 100%;
      width: max-content;
    }
  }

  @include phone-down {
    overflow-y: scroll;
  }
}

.sidebar {
  .sidebar-wrapper {
    width: $sidebar-width;
    height: 100%;
  }
}

.sidebar-transition-enter-active,
.sidebar-transition-leave-active {
  transition: transform 250ms ease-out, opacity 250ms linear;
}

.sidebar-transition-enter-from,
.sidebar-transition-leave-to {
  transform: translateX(100%);
  opacity: 0;
}

.sidebar-transition-enter-to,
.sidebar-transition-leave-from {
  transform: translateX(0);
  opacity: 1;
}
</style>
