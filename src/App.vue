<template>
  <Wordle />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Wordle from './components/Wordle.vue';

export default defineComponent({
  name: 'App',
  components: {
    Wordle
  }
});
</script>

<style lang="less">
html,
body {
  margin: 0;
  padding: 0;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: hsl(240, 3%, 7%);
  color: #fff;
  font-family: 'Clear Sans', Helvetica, Arial, sans-serif;
  height: calc(100vh - 60px);
  padding-top: 60px;
  text-align: center;
  width: 100%;
}
</style>