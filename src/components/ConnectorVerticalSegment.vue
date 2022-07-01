<template>
  <svg
    class="vertical-segment"
    xmlns="http://www.w3.org/2000/svg"
    :width="width"
    :height="height"
    :viewBox="viewBox"
    :style="style"
  >
    <line
      :x1="startingPoint.x"
      :y1="startingPoint.y"
      :x2="endingPoint.x"
      :y2="endingPoint.y"
      :stroke="color"
      :stroke-width="stroke"
      stroke-linecap="round"
    />
  </svg>
</template>
<script>
export default {
  name: "ConnectorVerticalSegment",
  props: ["X", "fromY", "toY", "stroke", "color", "z-index"],
  data() {
    return {
    }
  },
  computed: {
    padding() {
      return +this.stroke
    },
    width() {
      return +this.stroke * 2;
    },
    height() {
      return Math.abs(this.fromY - this.toY);
    },
    viewBox() {
      return `0 0 ${this.width} ${this.height}`;
    },
    startingPoint() {
      return {
        x: 0,
        y: this.fromY < this.toY ? 0 : this.height,
      };
    },
    endingPoint() {
      return {
        x: 0,
        y: this.fromY < this.toY ? this.height : 0,
      };
    },
    style() {
      return {
        left: `${this.startingPoint.x}px`,
        top: `${this.startingPoint.y}px`,
        position: 'absolute',
        zIndex: this.$props['z-index']
      };
    },
  },
};
</script>
