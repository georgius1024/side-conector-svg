<template>
  <div class="connector" :style="style">
    <VerticalSegment
      :color="color"
      :stroke="stroke"
      :z-index="100"
      :X="fromX"
      :fromY="fromY"
      :toY="toY"
    />
    <HorizontalSegment
      :color="color"
      :stroke="stroke"
      :z-index="100"
      :Y="toY"
      :fromX="fromX"
      :toX="toX"
    />
  </div>
</template>
<script>
import VerticalSegment from "./ConnectorVerticalSegment.vue";
import HorizontalSegment from "./ConnectorHorizontalSegment.vue";
export default {
  name: "Connector",
  components: {
    VerticalSegment,
    HorizontalSegment,
  },
  props: ["fromX", "fromY", "toX", "toY", "stroke", "color"],
  data() {
    return {
      padding: 0,
    };
  },
  computed: {
    width() {
      return Math.abs(this.fromX - this.toX) + this.padding * 2;
    },
    height() {
      return Math.abs(this.fromY - this.toY) + this.padding * 2;
    },
    viewBox() {
      return `0 0 ${this.width} ${this.height}`;
    },
    startingPoint() {
      return {
        x: this.fromX < this.toX ? this.padding : this.width - this.padding,
        y: this.fromY < this.toY ? this.padding : this.height - this.padding,
      };
    },
    endingPoint() {
      return {
        x: this.fromX < this.toX ? this.width - this.padding : this.padding,
        y: this.fromY < this.toY ? this.height - this.padding : this.padding,
      };
    },
    style() {
      return {
        left: `${this.startingPoint.x}px`,
        top: `${this.startingPoint.y}px`,
        width: `${this.width}px`,
        height: `${this.height}px`,
      };
    },
  },
};
</script>
<style>
.connector {
  position: absolute;
  outline: 1px solid red;
}
</style>
