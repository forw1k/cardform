<template>
  <div class="card">
    <div class="card__img">
      <img :src="card.src" class="card__pic" alt="Изображение товара" />
    </div>
    <div class="card__desc">
      <div class="card__name">{{ card.name }}</div>
      <div class="card__text">{{ cuttedDescription }}</div>
      <div class="card__price">{{ formattedPrice }} руб.</div>
    </div>
    <div @click="$emit('remove', card)" class="card__remove">
      <img
        src="../assets/icons/delete-icon.svg"
        class="card__icon"
        alt="удалить товар"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'my-card',
  props: {
    card: {
      type: Object,
      required: true
    }
  },
  computed: {
    formattedPrice () {
      return Number(this.card.price).toLocaleString('ru-RU')
    },
    cuttedDescription () {
      return this.card.description.slice(0, 120)
    }
  }
}
</script>

<style lang="scss" scoped>
.card {
  max-width: 33.2rem;
  max-height: 50rem;
  position: relative;
  background: #fffefb;
  box-shadow: 0 2rem 3rem rgba(0, 0, 0, 0.04), 0 0.6rem 1rem rgba(0, 0, 0, 0.02);
  border-radius: 0.4rem;
  cursor: pointer;
  word-break: break-all;
  &:hover {
    .card__remove {
      opacity: 1;
      visibility: visible;
    }
  }
  &__remove {
    display: flex;
    align-items: center;
    justify-content: center;
    position: absolute;
    opacity: 0;
    visibility: hidden;
    top: -1rem;
    right: -1rem;
    width: 3.2rem;
    height: 3.2rem;
    background: #ff8484;
    box-shadow: 0 0.2rem 0.4rem rgba(0, 0, 0, 0.1);
    border-radius: 1rem;
    cursor: pointer;
    &:hover {
      background: #f66868;
    }
    &:active {
      background: #ff8484;
    }
  }
  &__icon {
    width: 50%;
    height: 50%;
  }
  &__img {
    height: 20rem;
    width: 100%;
    margin-bottom: 2rem;
    flex-shrink: 0;
    overflow: hidden;
  }
  &__pic {
    border-radius: 0.4rem 0.4rem 0 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  &__desc {
    padding: 0 1.6rem 2rem 1.6rem;
    min-height: 20rem;
    display: flex;
    flex-direction: column;
  }
  &__name {
    font-size: 1.8rem;
    color: #3f3f3f;
    font-weight: 600;
    margin-bottom: 1.6rem;
  }
  &__text {
    font-size: 1.6rem;
    color: #3f3f3f;
    margin-bottom: 3.4rem;
    margin-bottom: auto;
    line-height: 1.25;
  }
  &__price {
    font-size: 2.4rem;
    font-weight: 600;
    color: #3f3f3f;
  }
}
@media (max-width: 768px) {
  .card {
    max-width: 100%;
  }
}
</style>
