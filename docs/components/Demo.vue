<template>
  <div
    :style="{
      display: 'flex',
      justifyContent: 'center',
      background: darkMode ? '#22272e' : '',
      padding: darkMode ? '10px 0' : '',
    }"
  >
    <calendar-heatmap
      :values="data"
      :end-date="endDate"
      :style="{
        'max-width': '675px',
        width: '100%',
      }"
      :round="round"
      :dark-mode="isDarkMode"
      :range-color="rangeColor"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType, ref, toRef } from "vue";
import { data } from "../../src/data";
import CalendarHeatmap from "../../src/components/CalendarHeatmap.vue";

export default defineComponent({
  name: "Demo",
  components: {
    CalendarHeatmap,
  },
  props: {
    initialRound: Number,
    orientation: {
      type: String as PropType<"horizontal">,
      default: "horizontal",
    },
    withSlider: Boolean,
    darkMode: Boolean,
    rangeColor: {
      type: Array as PropType<string[]>,
    },
  },
  setup(props) {
    const round = ref(
        props.initialRound !== undefined ? props.initialRound : 2
      ),
      isDarkMode = props.darkMode ? toRef(props, "darkMode") : false;

    return {
      data,
      round,
      isDarkMode,
      endDate: new Date("2021-08-01"),
    };
  },
});
</script>
