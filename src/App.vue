<template>
  <div class="wrapper"></div>
</template>

<script>
export default {
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
  }
}
</script>

<style lang="scss">
</style>
