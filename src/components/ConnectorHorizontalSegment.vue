<template>
  <svg
    class="horizontal-segment"
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
  name: "ConnectorHorizontalSegment",
  props: ["Y", "fromX", "toX", "stroke", "color", "z-index"],
  data() {
    return {
    };
  },
  computed: {
    strokeWidth() {
      return +this.stroke;
    },
    dX() {
      return Math.abs(this.fromX - this.toX)
    },
    width() {
      return this.dX + this.strokeWidth;
    },
    height() {
      return this.strokeWidth;
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
        x: this.dX + this.strokeWidth / 2,
        y: this.strokeWidth/2,
      };
    },
    style() {
      return {
        left: `${this.fromX -this.strokeWidth / 2}px`,
        top: `${this.Y -this.strokeWidth / 2}px`,
        position: "absolute",
        zIndex: this.$props["z-index"],
      };
    },
  },
};
</script>
