<template>
  <header
      :class="['base-header', {
        'scrolled': isScrolled
      }]"
  >
    <h1 class="base-header__title">Users List</h1>
  </header>
</template>

<script>
const HEADER_HEIGHT = 50
export default {
  name: "BaseHeader",
  data() {
    return {
      isScrolled: false,
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll)
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    handleScroll() {
      this.isScrolled = window.scrollY > HEADER_HEIGHT
    }
  }
}
</script>

<style
  lang="scss"
  scoped
>
$header-height: 50px;

.base-header {
  position: sticky;
  top: 0;
  width: 100%;
  height: $header-height;
  display: flex;
  align-items: center;
  justify-content: center;
  border-bottom: 1px solid #999;
  background: #eee;
  transition: .3s ease-in-out;
  z-index: 1;

  &.scrolled {
    transform: translateY(-$header-height);
  }

  .base-header__title {
    margin: 0;
  }
}
</style>