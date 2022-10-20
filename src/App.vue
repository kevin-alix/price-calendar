<template>
  <div id="app">
    <PriceCalendar :prices="prices" />
  </div>
</template>

<script>
import PriceCalendar from './components/PriceCalendar.vue'

export default {
  name: 'App',
  components: {
    PriceCalendar,
  },
  data() {
    const date = new Date()
    const year = date.getFullYear()
    const month = date.getMonth()

    return {
      prices: [
        {
          date: new Date(year, month, '14'),
          price: 'RM 129',
        },
        {
          date: new Date(year, month, '15'),
          price: 'RM 899',
        },
        {
          date: new Date(year, month, '16'),
          price: 'RM 39',
        },
        {
          date: new Date(year, month, '17'),
          price: 'RM 65',
        },
        {
          date: new Date(year, month, '18'),
          price: 'RM 79',
        },
        {
          date: new Date(year, month, '19'),
          price: 'RM 199',
        },
        {
          date: new Date(year, month, '20'),
          price: 'RM 799',
        },
        {
          date: new Date(year, month, '21'),
          price: 'RM 679',
        },
        {
          date: new Date(year, month, '22'),
          price: 'RM 69',
        },
        {
          date: new Date(year, month, '23'),
          price: 'RM 599',
        },
        {
          date: new Date(year, month, '24'),
          price: 'RM 199',
        },
        {
          date: new Date(year, month, '25'),
          price: 'RM 299',
        },
        {
          date: new Date(year, month, '26'),
          price: 'RM 79',
        },
        {
          date: new Date(year, month, '27'),
          price: 'RM 199',
        },
        {
          date: new Date(year, month, '28'),
          price: 'RM 99',
        },
        {
          date: new Date(year, month, '29'),
          price: 'RM 299',
        },
        {
          date: new Date(year, month, '30'),
          price: 'RM 399',
        },
      ],
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
