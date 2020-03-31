<template>
  <div class="is-container">
    <b-field class="is-success">
      <b-radio-button
        v-for="(interval, index) in intervals"
        :key="'interval'+index"
        v-model="selectedIndex"
        :native-value="index"
        type="is-info"
        size="is-small"
        :expanded="true"
      >
        <span>{{ (selectedIndex==index?intervalValue+' ':'') +interval.label}}</span>
      </b-radio-button>
    </b-field>
    <b-field>
      <b-slider
        :min="selectedInterval.min"
        :max="selectedInterval.max"
        ticks
        v-model="intervalValue"
        type="is-info"
        :tooltip="false"
        rounded="true"
      ></b-slider>
    </b-field>
  </div>
</template>

<script>
export default {
  props: {
    intervals: {
      type: Array,
      default: function() {
        return [
          { label: "Anni", prefix: "P", suffix: "Y", min: 1, max: 10 },
          { label: "Mesi", prefix: "P", suffix: "M", min: 1, max: 12 },
          { label: "Settimane", prefix: "P", suffix: "W", min: 1, max: 52 },
          { label: "Giorni", prefix: "P", suffix: "D", min: 1, max: 31 },
          { label: "Ore", prefix: "PT", suffix: "H", min: 1, max: 23 },
          { label: "Minuti", prefix: "PT", suffix: "M", min: 15, max: 59 }
        ];
      }
    }
  },
  data() {
    return {
      selectedIndex: 0,
      intervalValue: 15
    };
  },
  computed: {
    selectedInterval() {
      return this.intervals[this.selectedIndex];
    },
    isoInterval() {
      return (
        this.selectedInterval.prefix +
        this.intervalValue +
        this.selectedInterval.suffix
      );
    }
  },
  methods: {},
  watch: {
    selectedIndex(newValue, oldValue) {
      let newInterval = this.intervals[newValue];
      console.log(newInterval, this.intervalValue);
      if (
        !(
          newInterval.min <= this.intervalValue &&
          this.intervalValue <= newInterval.max
        )
      ) {
        this.intervalValue = newInterval.min;
        console.log(newInterval, this.intervalValue);
      } else {
        this.$emit("input", this.isoInterval);
      }
    },
    intervalValue(newValue, oldValue) {
      this.$emit("input", this.isoInterval);
    }
  }
};
</script>
<style scoped>
.is-container {
  position: relative;
  width: 100%;
  padding: 0.5rem;
}

.b-slider {
  width: 98%;
  margin: 0 auto;
}
</style>


