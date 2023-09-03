<template>
  <div class="wordle">
    <div class="guess">
      <div class="row" v-for="i in 5" :key="i">
        <div class="tile empty" v-for="j in 5" :key="j"></div>
      </div>
    </div>
    <div data-keyboard class="keyboard">
      <button class="key" data-key="Q">Q</button>
      <button class="key" data-key="W">W</button>
      <button class="key" data-key="E">E</button>
      <button class="key" data-key="R">R</button>
      <button class="key" data-key="T">T</button>
      <button class="key" data-key="Y">Y</button>
      <button class="key" data-key="U">U</button>
      <button class="key" data-key="I">I</button>
      <button class="key" data-key="O">O</button>
      <button class="key" data-key="P">P</button>
      <div class="space"></div>
      <button class="key" data-key="A">A</button>
      <button class="key" data-key="S">S</button>
      <button class="key" data-key="D">D</button>
      <button class="key" data-key="F">F</button>
      <button class="key" data-key="G">G</button>
      <button class="key" data-key="H">H</button>
      <button class="key" data-key="J">J</button>
      <button class="key" data-key="K">K</button>
      <button class="key" data-key="L">L</button>
      <div class="space"></div>
      <button data-enter class="key large">Enter</button>
      <button class="key" data-key="Z">Z</button>
      <button class="key" data-key="X">X</button>
      <button class="key" data-key="C">C</button>
      <button class="key" data-key="V">V</button>
      <button class="key" data-key="B">B</button>
      <button class="key" data-key="N">N</button>
      <button class="key" data-key="M">M</button>
      <button data-delete class="key large">
        <svg xmlns="http://www.w3.org/2000/svg" height="24" width="24" viewBox="0 0 24 24">
          <path fill="#fff" d="M22 3H7c-.69 0-1.23.35-1.59.88L0 12l5.41 8.11c.36.53.9.89 1.59.89h15c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm0 16H7.07L2.4 12l4.66-7H22v14zm-11.59-2L14 13.41 17.59 17 19 15.59 15.41 12 19 8.41 17.59 7 14 10.59 10.41 7 9 8.41 12.59 12 9 15.59z"></path>
        </svg>
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'WordleComponent'
});
</script>

<style scoped lang="less">
.wordle {
  .guess {
    display: inline-block;
    margin: 0 auto;
    .row {
      display: flex;
      grid-gap: 5px;
      margin-top: 5px;
      .tile {
        border: none;
        display: inline-flex;
        height: 75px;
        width: 75px;
        &.empty {
          border: 2px solid #3a3a3c;
        }
      }
    }
  }
  .keyboard {
    bottom: 10px;
    display: grid;
    gap: 0.25em;
    grid-auto-rows: 3em;
    grid-template-columns: repeat(20, minmax(auto, 1.25em));
    justify-content: center;
    left: 50%;
    position: absolute;
    transform: translateX(-50%);
  }
  .key {
    align-items: center;
    background-color: hsl(200, 1%, calc(51%));
    border: none;
    border-radius: 0.25em;
    color: white;
    cursor: pointer;
    display: flex;
    fill: white;
    font-size: inherit;
    grid-column: span 2;
    justify-content: center;
    padding: 0;
    text-transform: uppercase;
    user-select: none;
    &.large {
      grid-column: span 3;
    }
    > svg {
      height: 1.75em;
      width: 1.75em;
    }
    &:hover {
      --lightness-offset: 10%;
    }
    &:focus {
      --lightness-offset: 10%;
    }
  }
}
</style>