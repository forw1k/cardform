<template>
  <div class="filter">
    <div @click="openFilter" class="filter__title">
      <div class="filter__name">
        {{ selected.name }}
      </div>
      <div class="filter__img">
        <img src="../assets/icons/arrow-donw-icon.svg" class="filter__icon" />
      </div>
    </div>
    <div v-if="isFilterVisible" class="filter__hidden">
      <div
        v-for="option in options"
        :key="option.index"
        @click="selectOption(option)"
        class="filter__option"
      >
        {{ option.name }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'my-filter',
  props: {
    options: {
      type: Array
    },
    selected: {
      type: Object
    },
    isFilterVisible: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    selectOption (option) {
      this.$emit('select', option)
    },
    openFilter () {
      this.$emit('openFilter', true)
    }
  }
}
</script>

<style lang="scss" scoped>
.filter {
  position: absolute;
  right: 0;
  z-index: 222;
  background: #fffefb;
  box-shadow: 0 0.2rem 0.5rem rgba(0, 0, 0, 0.1);
  border-radius: 0.4rem;
  color: #b4b4b4;
  font-size: 1.2rem;
  cursor: pointer;
  transition: 0.5s;
  &__title {
    display: flex;
    align-items: center;
    padding: 0.8rem 1.6rem;
  }
  &__name {
    margin-right: 0.5rem;
  }
  &__option {
    padding: 0.8rem 1.6rem;
    &:hover {
      background: lightgrey;
      color: #fff;
    }
  }
}
</style>
