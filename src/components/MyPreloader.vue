<template>
  <div class="preloader">
    <img src="../assets/icons/loading-icon.svg" class="preloader__pic" />
  </div>
</template>

<script>
export default {
  name: 'my-preloader'
}
</script>

<style lang="scss" scoped>
.preloader {
  display: flex;
  align-items: center;
  justify-content: center;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0.7;
  background: #eeeeee;
  &__pic {
    width: 30rem;
  }
}
</style>
