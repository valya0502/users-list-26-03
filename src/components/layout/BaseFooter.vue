<template>
  <footer class="base-footer">
    <p>© 2024 Users List</p>
  </footer>
</template>

<script>
export default {
  name: "BaseFooter"
}
</script>

<style
  scoped
  lang="scss"
>
$footer-height: 50px;

.base-footer {
  position: sticky;
  bottom: 0;
  width: 100%;
  height: $footer-height;
  display: flex;
  align-items: center;
  justify-content: center;
  border-top: 1px solid #999;
  background: #eee;
}
</style>