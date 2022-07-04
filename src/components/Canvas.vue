<template>
  <div class="canvas" @click="movePoint">
    <Point :X="from.X" :Y="from.Y" />
    <Point :X="to.X" :Y="to.Y" />
    <Connector
      :fromX="from.X"
      :fromY="from.Y"
      :toX="to.X"
      :toY="to.Y"
      :stroke="6"
      color="#0093ff"
      :animated="true"
    />
  </div>
</template>
<script>
import Connector from "./Connector.vue";
import Point from "./Point.vue";

export default {
  components: {
    Connector,
    Point,
  },
  data() {
    return {
      from: { X: 0, Y: 0 },
      to: { X: 0, Y: 0 },
    };
  },
  created() {
    this.from.X = window.innerWidth / 2;
    this.from.Y = window.innerHeight / 2;
    this.to.X = this.from.X + 200;
    this.to.Y = this.from.Y - 200;
  },
  methods: {
    movePoint(e) {
      this.to.X = e.clientX;
      this.to.Y = e.clientY;
    },
  },
};
</script>
<style scoped>
.canvas {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}
</style>
