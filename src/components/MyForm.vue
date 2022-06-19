<template>
  <form class="form">
    <div class="form__item">
      <label class="form__label form__label_required"
        >Наименование товара</label
      >
      <input
        type="text"
        class="form__input"
        :class="{ form__input_error: nameFocusLost && missingName }"
        id="name-input"
        placeholder="Введите наименование товара"
        v-model="card.name"
        @blur="handleFocusOut"
      />
      <div v-if="nameFocusLost && missingName" class="form__error">
        Поле является обязательным
      </div>
    </div>
    <div class="form__item">
      <label class="form__label">Описание товара</label>
      <textarea
        type="text"
        class="form__textarea"
        placeholder="Введите описание товара"
        v-model="card.description"
      />
    </div>
    <div class="form__item">
      <label class="form__label form__label_required"
        >Ссылка на изображение товара</label
      >
      <input
        type="text"
        class="form__input"
        :class="{ form__input_error: srcFocusLost && missingSrc }"
        id="src-input"
        placeholder="Введите ссылку"
        v-model="card.src"
        @blur="handleFocusOut"
      />
      <div v-if="srcFocusLost && missingSrc" class="form__error">
        Поле является обязательным
      </div>
    </div>
    <div class="form__item">
      <label class="form__label form__label_required">Цена товара</label>
      <input
        type="number"
        class="form__input"
        :class="{ form__input_error: priceFocusLost && missingPrice }"
        id="price-input"
        placeholder="Введите цену"
        v-model="card.price"
        @blur="handleFocusOut"
      />
      <div v-if="priceFocusLost && missingPrice" class="form__error">
        Поле является обязательным
      </div>
    </div>
    <button
      @click.prevent="createCard"
      :disabled="isButtonDisabled"
      :class="{ form__button_disabled: isButtonDisabled }"
      class="form__button"
    >
      Добавить товар
    </button>
  </form>
</template>

<script>
export default {
  name: 'my-form',
  data () {
    return {
      card: {
        id: null,
        name: '',
        src: '',
        description: '',
        price: ''
      },
      attemptSubmit: false,
      nameFocusLost: false,
      srcFocusLost: false,
      priceFocusLost: false
    }
  },
  computed: {
    missingName () {
      return this.card.name === ''
    },
    missingSrc () {
      return this.card.src === ''
    },
    missingPrice () {
      return this.card.price === ''
    },
    isButtonDisabled () {
      if (!this.missingName && !this.missingPrice && !this.missingSrc) {
        return false
      }
      return true
    }
  },
  methods: {
    handleFocusOut (e) {
      if (e.target.id === 'name-input') {
        this.nameFocusLost = true
      }
      if (e.target.id === 'src-input') {
        this.srcFocusLost = true
      }
      if (e.target.id === 'price-input') {
        this.priceFocusLost = true
      }
    },
    createCard () {
      if (!this.isButtonDisabled) {
        this.card.id = Date.now()
        this.attemptSubmit = true
        this.$emit('create', this.card)
        this.$emit('addNotification', {
          name: 'Товар успешно добавлен!',
          id: this.card.id.toLocaleString()
        })
        this.card = {
          id: '',
          name: '',
          src: '',
          description: '',
          price: ''
        }
        this.attemptSubmit = false
        this.nameFocusLost = false
        this.srcFocusLost = false
        this.priceFocusLost = false
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.form {
  width: 33.2rem;
  height: fit-content;
  padding: 2.6rem 2.4rem;
  background: #fffefb;
  box-shadow: 0 2rem 3rem rgba(0, 0, 0, 0.04), 0 0.6rem 1rem rgba(0, 0, 0, 0.02);
  border-radius: 0.4rem;
  margin-right: 1.6rem;
  &__error {
    color: #ff8484;
    margin-top: 0.4rem;
  }
  &__item {
    display: flex;
    flex-direction: column;
    position: relative;
    margin-bottom: 2rem;
    &:last-child {
      margin-bottom: 2.2rem;
    }
  }
  &__label {
    color: #49485e;
    font-size: 1rem;
    margin-bottom: 0.4rem;
    width: fit-content;
    &_required {
      position: relative;
      &:after {
        content: "";
        position: absolute;
        top: 0;
        right: -0.5rem;
        width: 0.4rem;
        height: 0.4rem;
        background: #ff8484;
        border-radius: 50%;
      }
    }
  }
  &__input,
  &__textarea {
    padding: 1rem 1.6rem;
    box-shadow: 0 0.2rem 0.5rem rgba(0, 0, 0, 0.1);
    border-radius: 0.4rem;
    font-size: 1.2rem;
    color: #3f3f3f;
    &::placeholder {
      color: #b4b4b4;
    }
    &:focus {
      border: 1px solid #2491eb;
      box-shadow: 0 0.2rem 0.5rem rgba(36, 145, 235, 0.25);
    }
    &_error {
      border: 1px solid #ff8484;
    }
  }
  &__textarea {
    height: 10.8rem;
    font-family: "SourceSansPro", sans-serif;
    font-weight: 400;
    font-size: 1.2rem;
  }
  &__button {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    padding: 1rem 1.6rem;
    font-size: 1.2rem;
    color: #fff;
    font-family: "Inter", sans-serif;
    font-weight: 600;
    background: #7bae73;
    border-radius: 1rem;
    cursor: pointer;
    &:hover {
      background: #5ca152;
    }
    &:active {
      background: #7bae73;
    }
    &_disabled {
      color: #b4b4b4;
      background: #eeeeee;
      cursor: default;
      &:hover {
        background: #eeeeee;
      }
    }
  }
}
@media (max-width: 768px) {
  .form {
    margin-right: 0;
    margin-bottom: 1.6rem;
    width: 100%;
  }
}
@media (max-width: 500px) {
  .form {
    padding: 1rem;
  }
}
</style>
