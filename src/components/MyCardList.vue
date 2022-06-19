<template>
  <transition-group name="card-list-transition-animate" class="card-list">
    <MyCard
      v-for="card in cards"
      :key="card.id"
      :card="card"
      @remove="$emit('remove', card)"
    />
  </transition-group>
</template>

<script>
import MyCard from '@/components/MyCard'
export default {
  name: 'my-card-list',
  components: {
    MyCard
  },
  props: {
    cards: {
      type: Array,
      default: () => [],
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
.card-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1.6rem;
}
.card-list-transition-animate {
  &-enter {
    transform: translateY(10rem);
    opacity: 0;
  }
  &-enter-active {
    transition: all 0.5s ease;
  }
  &-enter-to {
    opacity: 1;
  }
  &-leave {
    height: 10rem;
    opacity: 1;
  }
  &-leave-active {
    transition: transform 0.5s ease, opacity 0.5s, height 0.5s;
  }
  &-leave-to {
    height: 0;
    transform: translateY(-10rem);
    opacity: 0;
  }

  &-move {
    transition: transform 0.5s ease;
  }
}
@media (max-width: 1024px) {
  .card-list {
    grid-template-columns: repeat(2, 1fr);
  }
}
@media (max-width: 500px) {
  .card-list {
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>
