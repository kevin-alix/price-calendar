<template>
  <VCalendar :attributes="attrs" />
</template>

<script>
import VCalendar from 'v-calendar/lib/components/calendar.umd'

export default {
  name: 'PriceCalendar',
  data() {
    const date = new Date();
    const year = date.getFullYear();
    const month = date.getMonth();
    const day = date.getDate();
    return {
      attrs: [
        {
          key: 'today',
          highlight: {
            color: 'red',
            fillMode: 'solid',
            // contentClass: 'italic',
          },
          dates: new Date(year, month, day),
        },
        {
          dates: { start: new Date(year, month, 14), end: new Date(year, month, 30) },
          dot: {
            color: 'red',
            class: 'price-text-below-date',
          },
          popover: {
            label: 'RM 775',
            hideIndicator: true,
          },
        },
      ],
    };
  },
  components: {
    VCalendar
  },
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .vc-container {
    /* --text-sm: 18px; */
  }
  .vc-day {
    margin: 2px;
  }
  .vc-day-content {
    width: 42px !important;
    height: 42px !important;
  }
  .vc-highlight {
    width: 100% !important;
    height: 100% !important;
  }
</style>
