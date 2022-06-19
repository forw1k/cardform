<template>
  <div class="wrapper">
    <MyNotification :notifications="notifications" />
    <div class="container">
      <div class="head">
        <div class="head__title">Добавление товара</div>
        <MyFilter
          @select="selectOption"
          @openFilter="openFilter"
          :isFilterVisible="isFilterVisible"
          :options="options"
          :selected="selected"
        />
      </div>
      <div class="content">
        <MyForm @create="createCard" @addNotification="addNotification" />
        <MyCardList @remove="removeCard" :cards="sortedCards" />
      </div>
    </div>
    <MyPreloader v-if="isLoading" />
  </div>
</template>

<script>
import MyFilter from '@/components/MyFilter'
import MyCardList from '@/components/MyCardList'
import MyForm from '@/components/MyForm'
import MyNotification from '@/components/MyNotification'
import MyPreloader from '@/components/MyPreloader'
export default {
  components: {
    MyFilter,
    MyCardList,
    MyForm,
    MyNotification,
    MyPreloader
  },
  name: 'App',
  data () {
    return {
      notifications: [],
      isLoading: false,
      options: [
        { name: 'По умолчанию', value: 'default' },
        { name: 'Макс. цена', value: 'maxPrice' },
        { name: 'Мин. цена', value: 'minPrice' },
        { name: 'По наименованию', value: 'byName' }
      ],
      selected: {
        name: 'По умолчанию',
        value: 'default'
      },
      isFilterVisible: false,
      cards: [
        {
          id: 1,
          src: 'https://img5.goodfon.ru/wallpaper/nbig/8/8b/abstraktsiia-kartinka-rendering-svetiashchiesia-volny-igra-s.jpg',
          name: 'Наименование товара',
          description:
            'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000
        },
        {
          id: 2,
          src: 'https://montessoriself.ru/wp-content/uploads/2014/09/kartochka-yabloko-1.jpg',
          name: 'Наименование товара',
          description:
            'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000
        },
        {
          id: 3,
          src: 'http://www.ixbt.com/short/images/2017/Jun/Chuwi-Best-Aspect-Ratio-768x576.jpg',
          name: 'Наименование товара',
          description:
            'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000
        },
        {
          id: 4,
          src: 'https://funart.pro/uploads/posts/2021-04/1617530962_45-p-oboi-yarkie-kartinki-46.jpg',
          name: 'Наименование товара',
          description:
            'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000
        },
        {
          id: 5,
          src: 'https://st.depositphotos.com/1103957/54919/i/600/depositphotos_549197270-stock-photo-horizontal-frame-mockup-75-70x50.jpg',
          name: 'Наименование товара',
          description:
            'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000
        },
        {
          id: 6,
          src: 'https://upload.wikimedia.org/wikipedia/commons/thumb/8/8c/Aspect-ratio-3x2.svg/1200px-Aspect-ratio-3x2.svg.png',
          name: 'Наименование товара',
          description:
            'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
          price: 10000
        }
      ]
    }
  },
  computed: {
    sortedCards () {
      if (this.selected.value === 'minPrice') {
        return [...this.cards].sort(
          (itemA, itemB) => itemA.price - itemB.price
        )
      }
      if (this.selected.value === 'maxPrice') {
        return [...this.cards].sort(
          (itemA, itemB) => itemB.price - itemA.price
        )
      }
      if (this.selected.value === 'byName') {
        return [...this.cards].sort((itemA, itemB) =>
          itemA.name.localeCompare(itemB.name)
        )
      }
      return this.cards
    }
  },
  methods: {
    preload (time) {
      this.isLoading = true
      setTimeout(() => {
        this.isLoading = false
      }, time)
    },
    addNotification (item) {
      this.notifications.unshift(item)
    },
    hideNotification () {
      const vm = this
      if (this.notifications.length) {
        setTimeout(() => {
          vm.notifications.splice(vm.notifications.length - 1, 1)
        }, 3000)
      }
    },
    removeCard (card) {
      this.cards = this.cards.filter((item) => item.id !== card.id)
      this.saveCardsToLocalStorage()
    },
    createCard (card) {
      this.cards.unshift(card)
      this.saveCardsToLocalStorage()
    },
    selectOption (option) {
      this.selected = option
    },
    openFilter () {
      this.isFilterVisible = true
    },
    hideFilter () {
      this.isFilterVisible = false
    },
    saveCardsToLocalStorage () {
      const newCardsList = JSON.stringify(this.cards)
      localStorage.setItem('cards', newCardsList)
    }
  },
  watch: {
    notifications () {
      this.hideNotification()
    }
  },
  mounted () {
    if (localStorage.cards) {
      this.cards = JSON.parse(localStorage.getItem('cards'))
    }
    this.preload(500)
    this.hideNotification()
    document.addEventListener('click', this.hideFilter, true)
  },
  beforeDestroy () {
    document.removeEventListener('click', this.hideFilter)
  }
}
</script>

<style lang="scss" scoped>
.wrapper {
  padding: 3.2rem;
  position: relative;
}
.content {
  display: flex;
}
.head {
  position: relative;
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  margin-bottom: 1.6rem;
  &__title {
    font-size: 2.5rem;
    line-height: 1.25;
    font-weight: 600;
  }
}
@media (max-width: 768px) {
  .wrapper {
    padding: 1.6rem;
  }
  .content {
    flex-direction: column;
  }
}
@media (max-width: 500px) {
  .head {
    &__title {
      width: 50%;
    }
  }
}
</style>
