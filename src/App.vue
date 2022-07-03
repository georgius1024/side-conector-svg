<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import Connector from "./components/Connector.vue";
import C1 from "./components/C1.vue";
import Point from "./components/Point.vue";
</script>

<template>
  <!-- <Connector
    fromX="100"
    fromY="100"
    toX="300"
    toY="300"
    stroke="6"
    color="#0093ff"
  /> -->
  <Point :X="100" :Y="100"/>
  <Point :X="300" :Y="500"/>
  <C1 />
  <!-- <Connector
    fromX="600"
    fromY="200"
    toX="400"
    toY="400"
    stroke="6"
    color="#0093ff"
  /> -->
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px;
  position: relative;
}
</style>
