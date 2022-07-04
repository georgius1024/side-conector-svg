<template>
  <svg
    class="wrapper"
    :class="{ animated }"
    :width="width"
    :height="height"
    :viewPort="`0 0 ${width} ${height}`"
    :style="wrapperStyle"
  >
    <marker
      id="triangle"
      viewBox="0 0 10 10"
      refX="5"
      refY="5"
      markerHeight="4"
      orient="auto"
      :fill="color"
    >
      <path d="M 0 0 L 10 5 L 0 10 z" />
    </marker>
    <marker
      id="dot"
      viewBox="0 0 10 10"
      refX="5"
      refY="5"
      markerWidth="2"
      markerHeight="2"
    >
      <circle cx="5" cy="5" r="5" :fill="color" />
    </marker>
    <polyline
      id="line"
      :points="points"
      fill="none"
      stroke-dasharray="8"
      stroke-dashoffset="0"
      stroke-linejoin="bevel"
      stroke-linecap="round"
      :stroke="color"
      :stroke-width="stroke"
      marker-end="url(#triangle)"
      marker-start="url(#dot)"
    ></polyline>
  </svg>
</template>
<script>
export default {
  props: {
    fromX: {
      type: Number,
      required: true,
    },
    fromY: {
      type: Number,
      required: true,
    },
    toX: {
      type: Number,
      required: true,
    },
    toY: {
      type: Number,
      required: true,
    },
    stroke: {
      type: Number,
      required: true,
    },
    color: {
      type: String,
      required: true,
    },
    animated: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    padding() {
      return 10
    },
    from() {
      return {
        X: this.fromX,
        Y: this.fromY,
      };
    },
    to() {
      return {
        X: this.toX,
        Y: this.toY,
      };
    },
    baseX() {
      return Math.min(this.from.X, this.to.X);
    },
    baseY() {
      return Math.min(this.from.Y, this.to.Y);
    },
    width() {
      return Math.abs(this.from.X - this.to.X);
    },
    height() {
      return Math.abs(this.from.Y - this.to.Y);
    },
    wrapperStyle() {
      return {
        top: this.baseY - this.padding,
        left: this.baseX - this.padding,
        width: this.width + 2 * this.padding,
        height: this.height + 2 * this.padding,
      };
    },
    points() {
      const firstJunction = {
        ...this.from,
        X: (this.from.X + this.to.X) / 2,
      };
      const secondJunction = {
        ...this.to,
        X: firstJunction.X,
      };
      const points = [this.from, firstJunction, secondJunction, this.to];
      return points
        .map((e) => this.translatePoint(e))
        .map((e) => `${e.X},${e.Y}`)
        .join(" ");
    },
  },
  methods: {
    translateX(X) {
      return X - this.baseX + this.padding;
    },
    translateY(Y) {
      return Y - this.baseY + this.padding;
    },
    translatePoint(point) {
      return {
        ...point,
        X: this.translateX(point.X),
        Y: this.translateY(point.Y),
      };
    },
  },
};
</script>
<style scoped>
.wrapper {
  position: absolute;
}
.wrapper.animated #line {
  animation: dash-offset 1s infinite linear;
}
@keyframes dash-offset {
  to {
    stroke-dashoffset: -32;
  }
}
</style>
