<template>
  <div class="wordle" :class="{ modalOpen: modal }">
    <div class="header">
      <h3>WORDLE</h3>
      <div class="level-switch">
        <select v-model="level" @change="changeLevel">
          <option disabled value="">Select Level</option>
          <option value="easy">Easy</option>
          <option value="normal">Normal</option>
          <option value="hard">Hard</option>
          <option value="expert">Expert</option>
        </select>
      </div>
    </div>

    <div class="game">
      <div class="guess">
        <div
          class="row"
          v-for="i in 6"
          :key="i"
          :class="{ shake: shakeRow[i] }"
        >
          <input
            v-for="j in 5"
            :key="j"
            class="tile"
            :class="{
              wrong: check[i - 1][j - 1] === -1,
              position: check[i - 1][j - 1] === 0,
              success: check[i - 1][j - 1] === 1,
            }"
            disabled
            v-model="guess[i - 1][j - 1]"
          />
        </div>
      </div>
      <div class="keyboard">
        <button
          class="key"
          :class="{
            wrong: letters[16] === -1,
            position: letters[16] === 0,
            success: letters[16] === 1,
          }"
          type="button"
          @click="addLetter('q')"
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
          type="button"
          @click="addLetter('w')"
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
          type="button"
          @click="addLetter('e')"
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
          type="button"
          @click="addLetter('r')"
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
          type="button"
          @click="addLetter('t')"
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
          type="button"
          @click="addLetter('y')"
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
          type="button"
          @click="addLetter('u')"
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
          type="button"
          @click="addLetter('i')"
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
          type="button"
          @click="addLetter('o')"
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
          type="button"
          @click="addLetter('p')"
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
          type="button"
          @click="addLetter('a')"
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
          type="button"
          @click="addLetter('s')"
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
          type="button"
          @click="addLetter('d')"
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
          type="button"
          @click="addLetter('f')"
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
          type="button"
          @click="addLetter('g')"
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
          type="button"
          @click="addLetter('h')"
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
          type="button"
          @click="addLetter('j')"
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
          type="button"
          @click="addLetter('k')"
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
          type="button"
          @click="addLetter('l')"
        >
          L
        </button>
        <div class="space"></div>
        <button class="key large" @click="submitGuess()" type="button">
          Enter
        </button>
        <button     
          class="key"
          :class="{
            wrong: letters[25] === -1,
            position: letters[25] === 0,
            success: letters[25] === 1,
          }"
          type="button"
          @click="addLetter('z')"
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
          type="button"
          @click="addLetter('x')"
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
          type="button"
          @click="addLetter('c')"
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
          type="button"
          @click="addLetter('v')"
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
          type="button"
          @click="addLetter('b')"
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
          type="button"
          @click="addLetter('n')"
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
          type="button"
          @click="addLetter('m')"
        >
          M
        </button>
        <button class="key large" @click="removeLetter()" type="button">
          <svg xmlns="http://www.w3.org/2000/svg" height="24" width="24" viewBox="0 0 24 24">
            <path fill="#fff" d="M22 3H7c-.69 0-1.23.35-1.59.88L0 12l5.41 8.11c.36.53.9.89 1.59.89h15c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm0 16H7.07L2.4 12l4.66-7H22v14zm-11.59-2L14 13.41 17.59 17 19 15.59 15.41 12 19 8.41 17.59 7 14 10.59 10.41 7 9 8.41 12.59 12 9 15.59z"></path>
          </svg>
        </button>
      </div>
    </div>

    <div class="alertbox" v-if="alert">{{ alertMessage }}</div>
  </div>

  <div class="modal" v-if="modal">
    <div class="modal-header">Game Over</div>
      <div class="modal-body">
        The word was:
        <div class="word">
          <div class="tile" v-for="i in 5" :key="i">
            {{ target.split("")[i - 1].toLocaleUpperCase() }}
          </div>
        </div>
        <h5 class="congratulations" v-if="guessRight">
          Congratulations! You guessed it correctly
        </h5>
        <h5 class="congratulations" v-else>
          You guessed it incorrectly. Try again!
        </h5>
        <h5 class="one-more-game">
          One more game?
        </h5>
        <div class="buttons">
          <button class="button" @click="restartGame()" type="button">YES</button>
          <button class="button" @click="restartGame()" type="button">MORE YES</button>
        </div>
      </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import words from '../data/words.json';
import easy from '../data/easy.json';
import normal from '../data/normal.json';
import hard from '../data/hard.json';
import expert from '../data/expert.json';

export default defineComponent({
  name: 'WordleComponent',
  data() {
    return {
      letters: [
        -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2,
        -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2
      ],
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
      targets: easy,
      row: 1,
      alertMessage: '',
      alert: false,
      shakeRow: [false, false, false, false, false, false],
      guessRight: false,
      modal: true,
      modalText: '',
      level: 'easy'
    }
  },
  beforeMount() {
    this.restartGame();
  },
  created() {
    window.addEventListener('keydown', (e) => {
      e.preventDefault();
      if (this.row !== 7) {
        if (this.guess[this.row - 1].length < 5) {
          if (
            (e.keyCode > 64 && e.keyCode < 91) ||
            (e.keyCode > 96 && e.keyCode < 123) ||
            e.keyCode === 222
          ) {
            this.addLetter(e.key);
          }
        }

        if (e.keyCode === 13) {
          this.submitGuess();
        }

        if (e.keyCode === 8 && this.guess[this.row - 1].length > 0) {
          this.removeLetter();
        }
      } else {
        setTimeout(() => { this.modal = true; }, 1000);
      }
    });
  },
  methods: {
    changeLevel() {
      this.restartGame();
    },
    restartGame() {
      this.letters = [-2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2, -2];
      this.guess = ['', '', '', '', '', ''];
      this.check = [
          [-2, -2, -2, -2, -2],
          [-2, -2, -2, -2, -2],
          [-2, -2, -2, -2, -2],
          [-2, -2, -2, -2, -2],
          [-2, -2, -2, -2, -2],
          [-2, -2, -2, -2, -2],
      ];

      this.words = words;
      switch (this.level) {
        case "easy":
          this.targets = easy;
          break;
        case "normal":
          this.targets = easy.concat(normal);
          break;
        case "hard":
          this.targets = easy.concat(normal, hard);
          break;
        case "expert":
          this.targets = easy.concat(normal, hard, expert);
          break;
        default:
          break;
      }
      this.target = this.targets[Math.floor(Math.random() * this.targets.length)];
      this.row = 1;
      this.guessRight = false;
      this.modal = false;
    },
    addLetter(letter: string) {
      if (this.row === 7) {
        setTimeout(() => { this.modal = true; }, 1000);
      }
      this.guess[this.row - 1] = this.guess[this.row - 1] + letter.toUpperCase();
    },
    removeLetter() {
      if (this.row === 7) {
        setTimeout(() => { this.modal = true; }, 1000);
      }
      this.guess[this.row - 1] = this.guess[this.row - 1].slice(0, -1);
    },
    submitGuess() {
      if (this.guess[this.row - 1].length < 5) {
        this.showAlert(false, "Please enter the 5 letters word", 1000);
        return;
      }
      this.validateGuess(this.guess[this.row - 1]);
    },
    validateGuess(val: string) {
      val = val.toLowerCase();

      if (this.target === val) {
        this.check[this.row - 1] = [1, 1, 1, 1, 1];
        this.showAlert(true, "Congratulations! You guessed it correctly", 1000);
        this.guessRight = true;
        this.row = 7;

        for (let i = 0; i < 5; i++) {
          if (val.charCodeAt(i) === 351) {
            this.letters[26] = 1;
          } else if (val.charCodeAt(i) === 246) {
            this.letters[27] = 1;
          } else if (val.charCodeAt(i) === 287) {
            this.letters[28] = 1;
          } else if (val.charCodeAt(i) === 231) {
            this.letters[29] = 1;
          } else if (val.charCodeAt(i) === 252) {
            this.letters[30] = 1;
          } else {
            this.letters[val.charCodeAt(i) - 97] = 1;
          }
        }

        setTimeout(() => { this.modal = true; }, 1000);

        return;
      }

      if (this.row === 7) {
        setTimeout(() => { this.modal = true; }, 1000);
      }

      const temp = this.target.split('');

      if (!this.words.includes(val)) {
        this.showAlert(false, "Word is not found", 1000);
        return;
      }

      for (let i = 0; i < 5; i++) {
        if (val.charCodeAt(i) === 351) {
          this.letters[26] = this.letters[26] === -2 ? -1 : this.letters[26];
        } else if (val.charCodeAt(i) === 246) {
          this.letters[27] = this.letters[27] === -2 ? -1 : this.letters[27];
        } else if (val.charCodeAt(i) === 287) {
          this.letters[28] = this.letters[28] === -2 ? -1 : this.letters[28];
        } else if (val.charCodeAt(i) === 231) {
          this.letters[29] = this.letters[29] === -2 ? -1 : this.letters[29];
        } else if (val.charCodeAt(i) === 252) {
          this.letters[30] = this.letters[30] === -2 ? -1 : this.letters[30];
        } else {
          this.letters[val.charCodeAt(i) - 97] =
            this.letters[val.charCodeAt(i) - 97] === -2 ? -1 : this.letters[val.charCodeAt(i) - 97];
        }
      }

      temp.forEach((letter: string, index: number) => {
        let foundIndex = -1;

        for (let i = 0; i < 5; i++) {
          if (letter === val.charAt(i) && i === index) {
            if (foundIndex > -1) {
              this.check[this.row - 1][foundIndex] = -2;
            }
            if (val.charCodeAt(i) === 351) {
              this.letters[26] = 1;
            } else if (val.charCodeAt(i) === 246) {
              this.letters[27] = 1;
            } else if (val.charCodeAt(i) === 287) {
              this.letters[28] = 1;
            } else if (val.charCodeAt(i) === 231) {
              this.letters[29] = 1;
            } else if (val.charCodeAt(i) === 252) {
              this.letters[30] = 1;
            } else {
              this.letters[val.charCodeAt(i) - 97] = 1;
            }
            this.check[this.row - 1][i] = 1;
            break;
          } else if (letter === val.charAt(i) && this.check[this.row - 1][i] === -2 && foundIndex === -1) {
            foundIndex = i;
            this.check[this.row - 1][i] = 0;
            if (val.charCodeAt(i) === 351) {
              this.letters[26] = this.letters[26] === 1 ? 1 : 0;
            } else if (val.charCodeAt(i) === 246) {
              this.letters[27] = this.letters[27] === 1 ? 1 : 0;
            } else if (val.charCodeAt(i) === 287) {
              this.letters[28] = this.letters[28] === 1 ? 1 : 0;
            } else if (val.charCodeAt(i) === 231) {
              this.letters[29] = this.letters[29] === 1 ? 1 : 0;
            } else if (val.charCodeAt(i) === 252) {
              this.letters[30] = this.letters[30] === 1 ? 1 : 0;
            } else {
              this.letters[val.charCodeAt(i) - 97] = this.letters[val.charCodeAt(i) - 97] === 1 ? 1 : 0;
            }
          }
        }
      });

      this.check[this.row - 1] = this.check[this.row - 1].map((el) => el === -2 ? -1 : el);

      if (this.row === 6) {
        setTimeout(() => { this.modal = true; }, 1000);
      }

      this.row++;
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
      }, 1000);
    }
  },
});
</script>

<style scoped lang="less">
.wordle {
  height: calc(100% - 30px);
  position: relative;
  &.modalOpen {
    filter: blur(10px);
    pointer-events: none;
  }
  .header {
    width: 100%;
    height: 55px;
    border-bottom: 2px solid #545454;
    margin: auto 0;
    h3 {
      display: inline-block;
      left: 50%;
      position: absolute;
      transform: translateX(-50%);
    }
    .level-switch {
      align-items: center;
      display: flex;
      float: right;
      height: 55px;
      margin-right: 20px;
      select {
        border-radius: 5px;
        color: green;
        font-size: 14px;
        font-weight: bold;
        height: 35px;
        padding: 0 5px;
      }
    }
  }
  .game {
    display: flex;
    flex-direction: column;
    .guess {
      display: inline-block;
      margin: 30px auto 0;
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
          transition: background-color 2s ease, transform 1s ease;
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
      left: 0;
      margin: 0 auto;
      position: fixed;
      right: 0;
      width: 90%;
    }
    .key {
      align-items: center;
      background-color: #7E8081;
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
  }
  .alertbox {
    background: #fff;
    border-radius: 10px;
    color: #000;
    font-weight: 700;
    left: 50%;
    max-width: 250px;
    padding: 10px;
    position: absolute;
    top: 60px;
    transform: translateX(-50%);
  }
  @media screen and (max-width: 430px) {
    .header {
      h3 {
        left: 10px;
        transform: translateX(0);
      }
      .language-switch {
        margin-right: 10px;
      }
    }
    .game {
      margin: 10px 0;
      .guess {
        .row {
          .tile {
            height: 65px;
            width: 65px;
          }
        }
      }
    }
  }
  @media screen and (max-width: 370px) {
    .game {
      .guess {
        .row {
          .tile {
            height: 50px;
            width: 50px;
          }
        }
      }
    }
  }
  @media screen and (max-width: 300px) {
    .header {
      .language-switch {
        margin-right: 0;
        button {
          width: 30px;
        }
      }
    }
    .game {
      .guess {
        .row {
          .tile {
            height: 40px;
            width: 40px;
          }
        }
      }
    }
  }
  @media screen and (max-height: 850px) {
    .game {
      .guess {
        margin: 20px auto;
      }
      .keyboard {
        margin: 0 auto;
      }
    }
  }
  @media screen and (max-height: 700px) {
    .game {
      .guess {
        .row {
          .tile {
            height: 50px;
            width: 50px;
          }
        }
      }
    }
  }
  @media screen and (max-height: 590px) {
    .game {
      .guess {
        .row {
          .tile {
            height: 40px;
            width: 40px;
          }
        }
      }
    }
  }
  @media screen and (max-height: 540px) {
    .game {
      .guess {
        .row {
          .tile {
            height: 30px;
            width: 30px;
          }
        }
      }
    }
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
.modal {
  background-color: hsl(240, 3%, 7%);
  border: 1px solid black;
  border-radius: 10px;
  left: 50%;
  max-width: 75%;
  position: fixed;
  text-align: center;
  top: 50%;
  transform: translate(-50%, -50%);
  transition: 200ms ease-in-out;
  width: 100%;
  z-index: 9999;
  &-header {
    font-size: 24px;
    padding-bottom: 15px;
  }
  &-body {
    font-size: 18px;
  }
  .word {
    display: flex;
    margin: 15px 5%;
    width: 90%;
    .tile {
      background: #538d4e;
      border: #000;
      flex-basis: calc(20% - 1px);
      font-size: 20px;
      font-weight: 700;
      line-height: 2;
      margin-right: 1px;
      padding: 15px;
    }
  }
  .buttons {
    padding-bottom: 10px;
    button {
      background: #000;
      border: 1px dashed #538d4e;
      color: #fff;
      cursor: pointer;
      font-size: 16px;
      margin-left: 10px;
      outline: none;
      padding: 5px 10px;
      transition: all .5s;
      &:hover {
        background: #538d4e;
        border-color: #fff;
      }
    }
    button:first-child {
      margin-left: -10px;
    }
  }
  @media screen and (max-width: 332px) {
    .word {
      margin: 15px 15%;
      width: 70%;
      .tile {
        font-size: 14px;
        padding: 10px;
      }
    }
  }
  @media screen and (max-width: 288px) {
    .word {
      margin: 15px 15%;
      width: 70%;
      .tile {
        font-size: 12px;
        padding: 10px;
      }
    }
  }
}
</style>
