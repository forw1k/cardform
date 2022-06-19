<template>
  <div class="notification">
    <transition-group name="notification-transition-animate" class="notification__list">
      <div
        v-for="notification in notifications"
        :key="notification.id"
        class="notification__content"
      >
        <div>
          {{ notification.name }}
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  name: 'my-notification',
  props: {
    notifications: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style lang="scss" scoped>
.notification {
  position: fixed;
  top: 5rem;
  right: 3rem;
  z-index: 22;
  &__content {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 20rem;
    height: 5rem;
    background-color: #3adb76;
    color: #fff;
    font-size: 1.4rem;
    margin-top: 1.6rem;
    &:last-child {
      margin-bottom: 0;
    }
  }
  &__list {
    display: flex;
    flex-direction: column-reverse;
  }
}
.notification-transition-animate {
  &-enter {
    transform: translateX(12rem);
    opacity: 0;
  }
  &-enter-active {
    transition: all 0.5s ease;
  }
  &-enter-to {
    opacity: 1;
  }
  &-leave {
    height: 5rem;
    opacity: 1;
  }
  &-leave-active {
    transition: transform 0.5s ease, opacity 0.5s, height 0.5s;
  }
  &-leave-to {
    height: 0;
    transform: translateX(12rem);
    opacity: 0;
  }

  &-move {
    transition: transform 0.5s ease;
  }
}
</style>
