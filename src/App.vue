<template>
  <div id="app">
    <!-- navbar-expand-sm allows to put the elements in nav inline -->
    <app-head></app-head>
    <br />
    <b-container class="mt-5">
      <router-view />
    </b-container>
  </div>
</template>
<script>
import Head from "@/components/Head.vue";

export default {
  components: {
    "app-head": Head,
  },
};
</script>

<style>
#app {
  font-family: "Gloria Hallelujah", cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fff;
  background-color: #2c3e50;
  height: 100vh;
}

.img404 {
  height: auto;
  width: 300px;
  position: relative;
}
</style>
