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
      this.attrs.forEach((attr) => {
        const dateList = document.querySelectorAll(
          `.${attr.key} > .vc-day-content`,
        )

        dateList.forEach((dateElement) => {
          dateElement.setAttribute('aria-price', attr.label)
        })
      })
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.vc-day {
  width: 46px !important;
  height: 50px !important;
}
.vc-day-content[aria-price] {
  color: #e00 !important;
  padding-bottom: 14px;
}
.vc-day-content[aria-price]:after {
  clear: both;
  display: block;
  content: attr(aria-price);
  font-size: 8px;
  position: absolute;
  bottom: 4px;
  color: black;
}
.vc-highlights + .vc-day-content[aria-price]:after {
  color: #fff;
}
.vc-day-content {
  width: 46px !important;
  height: 50px !important;
}
.vc-highlight {
  width: 46px !important;
  height: 46px !important;
}
.vc-day-content {
  --text-sm: 16px;
}
</style>
