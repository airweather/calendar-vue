<template>
  <div id="app">
    <button @click="toggle">{{ cssBinding ? 'Calendar' : 'CssBinding'}}</button>
    <CssBinding v-if="cssBinding" />
    <Calendar v-else/>
    <!-- <HelloWorld v-else msg="Hello Vue 3 + Vite" /> -->
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import CssBinding from './components/CssBinding.vue';
import Calendar from './components/Calendar.vue';
export default {
  data() {
    return {
      cssBinding:true
    }
  },
  components: {
    HelloWorld,
    Calendar,
    CssBinding
  },
  methods: {
    toggle() {
      if(this.cssBinding) this.cssBinding=!this.cssBinding
      else this.cssBinding = true;
    }
  }
};
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>