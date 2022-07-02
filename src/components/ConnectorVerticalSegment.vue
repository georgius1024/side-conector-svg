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
      :stroke-width="strokeWidth"
      stroke-linecap="round"
    />
  </svg>
</template>
<script>
export default {
  name: "ConnectorVerticalSegment",
  props: ["X", "fromY", "toY", "stroke", "color", "z-index"],
  data() {
    return {};
  },
  computed: {
    strokeWidth() {
      return +this.stroke;
    },
    dY() {
      return Math.abs(this.fromY - this.toY);
    },
    width() {
      return this.strokeWidth;
    },
    height() {
      return this.dY + this.strokeWidth;
    },
    viewBox() {
      return `0 0 ${this.width} ${this.height}`;
    },
    startingPoint() {
      return {
        x: this.strokeWidth / 2,
        y: this.strokeWidth / 2,
      };
    },
    endingPoint() {
      return {
        x: this.strokeWidth / 2,
        y: this.dY + this.strokeWidth/2,
      };
    },
    style() {
      return {
        left: `${this.X - this.strokeWidth / 2}px`,
        top: `${this.fromY -this.strokeWidth / 2}px`,
        position: "absolute",
        zIndex: this.$props["z-index"],
      };
    },
  },
};
</script>
