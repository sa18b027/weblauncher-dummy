<template>
  <div id="app">
    <!-- <WebGazer @update="onUpdate" :off="false" /> -->
    <!-- <Favorites
      @update="onUpdate"
      :off="false"
      v-bind:currentX="currentX"
      v-bind:currentY="currentY"
    /> -->
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view />
  </div>
</template>
<script>
//import WebGazer from "@/components/WebGazer.vue";
//import Keyboard
// import Favorites from "@/components/Favorites.vue";

import { mapMutations } from "vuex";

export default {
  name: "App",
  // components: {WebGazer},
  // components: { Favorites },
  data: () => ({
    windowHeight: 0,
    windowWidth: 0,
    currentX: 0,
    currentY: 0,
  }),

  created: function() {
    this.windowHeight = window.innerHeight;
    this.windowWidth = window.innerWidth;
    window.addEventListener("mousemove", this.onUpdate);
  },
  destroyed: function() {
    window.removeEventListener("mousemove", this.onUpdate);
  },
  methods: {
    ...mapMutations(["setCurrentCoor"]),
    onUpdate(event) {
      this.currentX = event.clientX;
      this.currentY = event.clientY;
      this.setCurrentCoor({
        x: this.currentX,
        y: this.currentY,
      });
    },
  },
};
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
} */
</style>
