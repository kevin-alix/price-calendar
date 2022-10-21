<template>
  <v-date-picker
    :attributes="attrs"
    :min-date="minDate"
    v-model="range"
    is-range
    v-on="changeDate()"
  />
</template>

<script>
import VDatePicker from 'v-calendar/lib/components/date-picker.umd'

const getIdFromDate = (date) =>
  'id-' +
  date.getFullYear() +
  '-' +
  (date.getMonth() + 1) +
  '-' +
  date.getDate()

export default {
  name: 'PriceCalendar',
  data() {
    const date = new Date()
    const year = date.getFullYear()
    const month = date.getMonth()

    return {
      attrs: [
        ...this.prices.map((priceInfo) => ({
          key: getIdFromDate(priceInfo.date),
          label: priceInfo.price,
          content: 'red',
          class: 'day-content-with-price',
          dates: priceInfo.date,
          customData: {
            id: getIdFromDate(priceInfo.date),
            ...priceInfo,
          },
        })),
      ],
      range: {
        start: new Date(year, month, 11),
        end: new Date(year, month, 27),
      },
      minDate: new Date(year, month, 6),
    }
  },
  props: {
    prices: Array,
  },
  components: {
    VDatePicker,
  },
  mounted() {
    this.changeDate()
  },
  methods: {
    changeDate() {
      const dateList = document.querySelectorAll('.vc-day')

      dateList.forEach((dateElement) => {
        this.attrs.forEach((attr) => {
          if (dateElement.classList.contains(attr.key)) {
            dateElement.setAttribute('aria-price', attr.label)
          }
        })
      })
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.day-content-with-price {
  padding-top: 3px;
  height: 100%;
  font-weight: bold;
}
.vc-day {
  width: 46px !important;
  height: 46px !important;
}
.day-content-with-price {
  cursor: pointer;
  border-radius: var(--rounded-full);
}
.day-content-with-price:hover {
  background: #eee;
}
.selected-date {
  background: #e55;
}
.selected-date:hover {
  background: #e55;
}
.vc-day-content {
  width: 46px !important;
  height: 46px !important;
}
.vc-highlight {
  width: 100% !important;
  height: 100% !important;
}
.vc-highlights + div > .day-with-price {
  color: #fff;
}
.vc-highlights + div > .day-with-price + div {
  color: #fff;
}
.selected-date.day-content-with-price > .day-with-price {
  color: #fff;
}
.selected-date.day-content-with-price > .day-with-price + div {
  color: #fff;
}
.day-with-price {
  color: #e55;
}
</style>
