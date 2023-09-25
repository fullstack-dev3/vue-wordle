<template>
  <div class="loading" v-if="loading">
    <img v-bind:src="require('./data/wordle.png')" />
  </div>
  <Wordle v-else />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Wordle from './components/Wordle.vue';

export default defineComponent({
  name: 'App',
  components: {
    Wordle
  },
  data() {
    return {
      loading: true
    }
  },
  created() {
    setTimeout(() => {
      this.loading = false;
    }, 1000);
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
  height: 100vh;
  overflow-x: hidden;
  overflow-y: auto;
  text-align: center;
  width: 100%;
}
.loading {
  display: flex;
  height: 100vh;
  justify-content: center;
}
</style>