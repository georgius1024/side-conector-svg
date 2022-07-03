<template>
  <svg class="point" width="10" height="10" viewPort="0 0 10 10" :style="style">
    <line x1="0" y1="0" x2="10" y2="10" stroke="currentColor" stroke-width="1" />
    <line x1="10" y1="0" x2="0" y2="10" stroke="currentColor" stroke-width="1" />
  </svg>
</template>
<script>
export default {
  props: ["X", "Y"],
  computed: {
    style() {
      return {
        position: "absolute",
        left: `${this.X - 5}px`,
        top: `${this.Y - 5}px`,
      };
    },
  },
};
</script>
<style scoped>
.point {
  color: transparent;
  z-index: 100000;
}
.point:hover {
  color: #333;
}
</style>