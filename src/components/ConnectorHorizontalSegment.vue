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
    padding() {
      return +this.stroke
    },
    width() {
      return Math.abs(this.fromX - this.toX);
    },
    height() {
      return this.stroke;
    },
    viewBox() {
      return `0 0 ${this.width} ${this.height}`;
    },
    startingPoint() {
      return {
        x: this.fromX < this.toX ? 0 : this.width,
        y: 0,
      };
    },
    endingPoint() {
      return {
        x: this.fromX < this.toX ? this.width : 0,
        y: 0,
      };
    },
    style() {
      return {
        left: `${this.startingPoint.x}px`,
        top: `${-(this.startingPoint.y) + (+this.Y)}px`,
        position: "absolute",
        zIndex: this.$props["z-index"],
      };
    },
  },
};
</script>
