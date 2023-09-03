<template>
  <div class="wordle">
    <div class="header">
      <h3>WORDLE</h3>
    </div>
    <div class="guess">
      <div
        class="row"
        v-for="i in 6"
        :key="i"
        :class="{ shake: shakeRow[i] }"
      >
        <input
          :key="j"
          class="tile"
          :class="{
            wrong: check[i - 1][j - 1] === -1,
            position: check[i - 1][j - 1] === 0,
            success: check[i - 1][j - 1] === 1,
          }"
          disabled
          v-for="j in 5"
          v-model="guess[i - 1][j - 1]"
        />
      </div>
    </div>
    <div data-keyboard class="keyboard">
      <button
        class="key"
        :class="{
          wrong: letters[16] === -1,
          position: letters[16] === 0,
          success: letters[16] === 1,
        }"
      >
        Q
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[22] === -1,
          position: letters[22] === 0,
          success: letters[22] === 1,
        }"
      >
        W
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[4] === -1,
          position: letters[4] === 0,
          success: letters[4] === 1,
        }"
      >
        E
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[17] === -1,
          position: letters[17] === 0,
          success: letters[17] === 1,
        }"
      >
        R
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[19] === -1,
          position: letters[19] === 0,
          success: letters[19] === 1,
        }"
      >
        T
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[24] === -1,
          position: letters[24] === 0,
          success: letters[24] === 1,
        }"
      >
        Y
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[20] === -1,
          position: letters[20] === 0,
          success: letters[20] === 1,
        }"
      >
        U
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[8] === -1,
          position: letters[8] === 0,
          success: letters[8] === 1,
        }"
      >
        I
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[14] === -1,
          position: letters[14] === 0,
          success: letters[14] === 1,
        }"
      >
        O
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[15] === -1,
          position: letters[15] === 0,
          success: letters[15] === 1,
        }"
      >
        P
      </button>
      <div class="space"></div>
      <button
        class="key"
        :class="{
          wrong: letters[0] === -1,
          position: letters[0] === 0,
          success: letters[0] === 1,
        }"
      >
        A
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[18] === -1,
          position: letters[18] === 0,
          success: letters[18] === 1,
        }"
      >
        S
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[3] === -1,
          position: letters[3] === 0,
          success: letters[3] === 1,
        }"
      >
        D
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[5] === -1,
          position: letters[5] === 0,
          success: letters[5] === 1,
        }"
      >
        F
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[6] === -1,
          position: letters[6] === 0,
          success: letters[6] === 1,
        }"
      >
        G
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[7] === -1,
          position: letters[7] === 0,
          success: letters[7] === 1,
        }"
      >
        H
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[9] === -1,
          position: letters[9] === 0,
          success: letters[9] === 1,
        }"
      >
        J
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[10] === -1,
          position: letters[10] === 0,
          success: letters[10] === 1,
        }"
      >
        K
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[11] === -1,
          position: letters[11] === 0,
          success: letters[11] === 1,
        }"
      >
        L
      </button>
      <div class="space"></div>
      <button data-enter class="key large">Enter</button>
      <button
        class="key"
        :class="{
          wrong: letters[25] === -1,
          position: letters[25] === 0,
          success: letters[25] === 1,
        }"
      >
        Z
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[23] === -1,
          position: letters[23] === 0,
          success: letters[23] === 1,
        }"
      >
        X
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[2] === -1,
          position: letters[2] === 0,
          success: letters[2] === 1,
        }"
      >
        C
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[21] === -1,
          position: letters[21] === 0,
          success: letters[21] === 1,
        }"
      >
        V
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[1] === -1,
          position: letters[1] === 0,
          success: letters[1] === 1,
        }"
      >
        B
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[13] === -1,
          position: letters[13] === 0,
          success: letters[13] === 1,
        }"
      >
        N
      </button>
      <button
        class="key"
        :class="{
          wrong: letters[12] === -1,
          position: letters[12] === 0,
          success: letters[12] === 1,
        }"
      >
        M
      </button>
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
import words from '../data/words.json';
import targets from '../data/targets.json';

export default defineComponent({
  name: 'WordleComponent',
  data() {
    return {
      letters: [-2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2],
      guess: ['', '', '', '', '', ''],
      check: [
        [-2, -2, -2, -2, -2],
        [-2, -2, -2, -2, -2],
        [-2, -2, -2, -2, -2],
        [-2, -2, -2, -2, -2],
        [-2, -2, -2, -2, -2],
        [-2, -2, -2, -2, -2],
      ],
      words: words,
      target: '',
      targets: targets,
      row: 1,
      alertMessage: '',
      alert: false,
      shakeRow: [false, false, false, false, false, false],
    }
  },
  beforeMount() {
    this.target = this.targets[Math.floor(Math.random() * this.targets.length)];
  },
  created() {
    window.addEventListener('keydown', (e) => {
      if (this.row !== 7) {
        if (e.keyCode === 13 && this.guess[this.row - 1].length < 5) {
          this.showAlert(false, 'Complete the word!', 1500);
        }
        if (this.guess[this.row - 1].length < 5) {
          if (((e.keyCode > 64 && e.keyCode < 91) || (e.keyCode > 96 && e.keyCode < 123))) {
            this.guess[this.row - 1] = this.guess[this.row - 1] + e.key;
          }
        }

        if (e.keyCode === 13 && this.guess[this.row - 1].length === 5) {
          this.validateGuess(this.guess[this.row - 1]);
        }

        if (e.keyCode === 8 && this.guess[this.row - 1].length > 0) {
          this.guess[this.row - 1] = this.guess[this.row - 1].slice(0, -1);
        }
      } else {
        this.showAlert(false, 'Gameover! The word was ' + this.target + '... Refresh to restart', 1500);
      }
    });
  },
  methods: {
    validateGuess(val: string) {
      if (this.target === val) {
        this.check[this.row - 1] = [1, 1, 1, 1, 1];
        this.showAlert(true, 'Congratulations! You win!', 1500);
        this.row = 7;
        this.updateLetters(val);
        return;
      }

      val = val.toLowerCase();

      const temp = this.target.split('');
      if (!words.includes(val)) {
        this.showAlert(false, 'Word is not in word list', 1500);
        return;
      }

      this.updateLetters(val);

      for (let i = 0; i < 5; i++) {
        if (val.charAt(i) === temp[i]) {
          this.check[this.row - 1][i] = 1;
        } else if (temp.includes(val.charAt(i))) {
          this.check[this.row - 1][i] = 0;
        } else {
          this.check[this.row - 1][i] = -1;
        }
      }

      if (this.row === 6) {
        this.showAlert(false, 'Gameover! The word was ' + this.target + '... Refresh to restart', 3000);
      }

      this.row++;
    },
    updateLetters(val: string) {
      const temp = this.target.split('');
      for (let i = 0; i < 5; i++) {
        if (val.charAt(i) === temp[i]) {
          this.letters[val.charCodeAt(i) - 97] = 1;
        } else if (temp.includes(val.charAt(i))) {
          this.letters[val.charCodeAt(i) - 97] = 0;
        } else {
          this.letters[val.charCodeAt(i) - 97] = -1;
        }
      }
    },
    showAlert(type: boolean, message: string, duration: number) {
      if (!type) {
        this.shake();
      }

      this.alertMessage = message
      this.alert = true;

      setTimeout(() => {
        this.alert = false;
      }, duration);
    },
    shake() {
      this.shakeRow[this.row] = true;
      setTimeout(() => {
        this.shakeRow[this.row] = false;
      }, 1500);
    }
  },
});
</script>

<style scoped lang="less">
.wordle {
  height: calc(100% - 50px);
  position: relative;
  .header {
    border-bottom: 2px solid #fff;
    height: 30px;
    margin: auto 0;
    width: 100%;
  }
  .guess {
    display: inline-block;
    margin: 0 auto;
    .row {
      display: flex;
      grid-gap: 5px;
      margin-top: 5px;
      &.shake {
        animation: shake 250ms ease-in-out;
      }
      .tile {
        background: transparent;
        border: none;
        border: 2px solid #3a3a3c;
        caret-color: transparent;
        color: #fff;
        display: inline-flex;
        font-size: 24px;
        font-weight: 600;
        height: 75px;
        padding: 0;
        text-align: center;
        text-transform: uppercase;
        transition: background-color 4s ease, transform 1s ease;
        width: 75px;
        &.success {
          background-color: #538d4e;
          transform: rotateX(-180deg) scaleY(-1);
        }
        &.position {
          background-color: #b59f3b;
          transform: rotateX(-180deg) scaleY(-1);
        }
        &.wrong {
          background-color: #939598;
          transform: rotateX(-180deg) scaleY(-1);
        }
        &:hover {
          cursor: pointer;
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
    font-size: 14px;
    font-weight: 700;
    grid-column: span 2;
    justify-content: center;
    padding: 0;
    text-transform: uppercase;
    user-select: none;
    &.success {
      background-color: #538d4e;
    }
    &.position {
      background-color: #b59f3b;
    }
    &.wrong {
      background-color: #3a3a3c;
    }
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
  .alertbox {
    background: #fff;
    border-radius: 10px;
    color: #000;
    font-weight: 700;
    height: 30px;
    left: 50%;
    padding: 10px 10px 0;
    position: absolute;
    top: 60px;
    transform: translateX(-50%);
  }
  @keyframes shake {
    10% {
      transform: translateX(-5%);
    }
    30% {
      transform: translateX(5%);
    }
    50% {
      transform: translateX(-7.5%);
    }
    70% {
      transform: translateX(7.5%);
    }
    90% {
      transform: translateX(-5%);
    }
    100% {
      transform: translateX(0);
    }
  }
}
</style>