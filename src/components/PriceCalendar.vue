<template>
  <v-calendar :attributes="attrs">
    <template v-slot:day-content="{ day, attributes }">
      <div
        :class="
          'day-content-with-price' +
          (selectedDate == attr.customData.id ? ' selected-date' : '')
        "
        v-for="attr in attributes"
        @click="selectDate(attr.customData.id)"
        :id="attr.customData.id"
        :key="attr.key"
      >
        <span class="day-label text-sm day-with-price">{{ day.day }}</span>
        <div class="flex-grow overflow-y-auto overflow-x-auto">
          <div
            class="text-xs leading-tight rounded-sm p-1 mt-0 mb-1"
            style="font-size: 8px;"
            :class="attr.customData.class"
          >
            {{ attr.customData.price }}
          </div>
        </div>
      </div>
    </template>
  </v-calendar>
</template>

<script>
import VCalendar from 'v-calendar/lib/components/calendar.umd'

export default {
  name: 'PriceCalendar',
  data() {
    const date = new Date()
    const getIdFromDate = (date) =>
      'id' + date.getYear() + date.getMonth() + date.getDate()
    const selectedDate = getIdFromDate(date)

    return {
      attrs: [
        ...this.prices.map((priceInfo) => ({
          key: priceInfo.date.toString(),
          dates: priceInfo.date,
          customData: {
            id: getIdFromDate(priceInfo.date),
            ...priceInfo,
          },
        })),
      ],
      selectedDate: selectedDate,
    }
  },
  props: {
    prices: Array,
  },
  components: {
    VCalendar,
  },
  methods: {
    selectDate(id) {
      this.selectedDate = id
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
