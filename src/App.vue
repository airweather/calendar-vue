<template>
  <div id="app">
    <button @click="toggle">{{ test ? 'Calendar' : 'Test'}}</button>
    <Test v-if="test" />
    <Calendar v-else/>
    <!-- <HelloWorld v-else msg="Hello Vue 3 + Vite" /> -->
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import Test from './components/Test.vue';
import Calendar from './components/Calendar.vue';
export default {
  data() {
    return {
      test:true
    }
  },
  components: {
    HelloWorld,
    Calendar,
    Test
  },
  methods: {
    toggle() {
      if(this.test) this.test=!this.test
      else this.test = true;
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