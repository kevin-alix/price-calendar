<template>
  <v-calendar :attributes="attrs">
    <template v-slot:day-content="{ day, attributes }">
      <div
        class="flex flex-col h-full z-10 overflow-hidden"
        v-for="attr in attributes"
        :key="attr.key"
      >
        <span class="day-label text-sm day-with-price" >{{ day.day }}</span>
        <div class="flex-grow overflow-y-auto overflow-x-auto">
          <div
            class="text-xs leading-tight rounded-sm p-1 mt-0 mb-1"
            style="font-size: 8px"
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
    const date = new Date();
    const updatedPrices = this.prices.map((value) => {
      if (value.date.getDate() === date.getDate()) {
        return {
          key: value.toString(),
          ...value,
          highlight: {
            color: 'red',
            fillMode: 'solid',
          },
        };
      }

      return {
        key: value.toString(),
        ...value,
      };
    });

    return {
      attrs: [
        ...updatedPrices.map(priceInfo => ({
          key: priceInfo.key,
          highlight: priceInfo.highlight,
          dates: priceInfo.date,
          customData: priceInfo,
        })),
      ],
    };
  },
  components: {
    VCalendar,
  },
  props: {
    prices: Array,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .vc-day {
    margin: 2px;
    width: 42px !important;
    height: 42px !important;
  }
  .vc-day-content {
    width: 42px !important;
    height: 42px !important;
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
  .day-with-price {
    color: #f00;
  }

</style>
