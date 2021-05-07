<template>
  <div class="simon">
    <div
      :class="[
        disable ? 'container disable' : 'container',
        pressed && btn === 1 ? 'red' : '',
        pressed && btn === 2 ? 'blue' : '',
        pressed && btn === 3 ? 'yellow' : '',
        pressed && btn === 4 ? 'green' : '',
      ]"
    >
      <div
        id="btn_1"
        @click="userPress(1, true)"
        :class="{ press: pressed && btn === 1 }"
      ></div>
      <div
        id="btn_2"
        @click="userPress(2, true)"
        :class="{ press: pressed && btn === 2 }"
      ></div>
      <div
        id="btn_3"
        @click="userPress(3, true)"
        :class="{ press: pressed && btn === 3 }"
      ></div>
      <div
        id="btn_4"
        @click="userPress(4, true)"
        :class="{ press: pressed && btn === 4 }"
      ></div>
    </div>
    <audio id="1" src="../audio/1.ogg"></audio>
    <audio id="2" src="../audio/2.ogg"></audio>
    <audio id="3" src="../audio/3.ogg"></audio>
    <audio id="4" src="../audio/4.ogg"></audio>
    <SimonDashboard />
  </div>
</template>

<script>
import SimonDashboard from "./SimonDashboard";
export default {
  name: "Simon",
  components: {
    SimonDashboard,
  },
  data() {
    return {
      disable: true,
      started: false,
      pressed: false,
      btn: 0,
      userClicks: [],
      userGuess: 0,
      generatedClicks: [],
      clicksCount: 1,
      interval: 1500,
      message: "Ты готов ?",
    };
  },
  methods: {
    generateClicks() {
      this.started = true;
      this.message = "Очередь програмы";
      this.disable = true;
      setTimeout(() => {
        for (let i = 0; i < this.clicksCount; i++) {
          this.generatedClicks.push(Math.floor(Math.random() * 4) + 1);
        }
        this.programPress();
      }, 1000);
    },
    programPress() {
      for (let v = 0; v < this.clicksCount; v++) {
        setTimeout(() => {
          this.userPress(this.generatedClicks[v]);
          v === this.clicksCount - 1
            ? ((this.message = "Твоя очередь"), (this.disable = false))
            : "";
        }, this.interval * v);
      }
    },
    userPress(v, u) {
      if (u) {
        this.userClicks.push(v);
        if (this.generatedClicks[this.userGuess] !== v) {
          this.gameOver();
        } else if (this.userClicks.length >= this.generatedClicks.length) {
          this.nextRound();
          this.generateClicks();
        } else {
          this.userGuess++;
        }
      }
      var audio = document.getElementById(v);
      audio.play();
      this.pressed = !this.pressed;
      this.btn = v;
      setTimeout(() => {
        this.pressed = false;
        this.btn = 0;
      }, 100);
    },
    gameOver() {
      this.message = `Вы проиграли в ${this.generatedClicks.length} раунде`;
      this.disable = true;
      this.userGuess = 0;
      this.clicksCount = 1;
      this.userClicks.length = 0;
      this.generatedClicks.length = 0;
      this.started = false;
    },
    nextRound() {
      this.clicksCount++;
      this.userGuess = 0;
      this.generatedClicks.length = 0;
      this.userClicks.length = 0;
    },
  },
};
</script>

<style  lang="scss" scoped>
.simon {
  display: flex;
  flex-direction: row;
  text-align: center;
  width: 800px;
  margin: auto;
  .disable {
    pointer-events: none;
  }
  .container[data-v-f3f3eg9] {
    flex-direction: column !important;
  }
  .red {
    box-shadow: -16px -1px 16px #ff5643 !important;
  }
  .green {
    box-shadow: 16px 1px 16px #bede15 !important;
  }
  .yellow {
    box-shadow: -16px -1px 16px #feef33 !important;
  }
  .blue {
    box-shadow: 16px 1px 16px dodgerblue !important;
  }
  .container {
    display: flex;
    width: 350px;
    min-width: 350px;
    min-height: 350px;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;
    align-items: center;
    margin: 0 auto;
    border-radius: 100px;
    padding: 10px;
    box-shadow: 5px 1px 12px rgba(50, 50, 93, 0.25),
      -5px -1px 12px rgba(50, 50, 93, 0.25);
    div {
      width: 154px;
      height: 154px;
      opacity: 0.8;
      border-radius: 10px;
      box-shadow: rgba(0, 0, 0, 0.19) 0px 10px 20px,
        rgba(0, 0, 0, 0.23) 0px 6px 6px;
    }
    .press {
      box-shadow: rgba(50, 50, 93, 0.25) 0px 30px 60px -12px inset,
        rgba(0, 0, 0, 0.3) 0px 18px 36px -2px inset;
      opacity: 1;
    }
    #btn_1 {
      background: #ff5643;
      border-top-left-radius: 154px;
    }
    #btn_2 {
      background: dodgerblue;
      border-top-right-radius: 154px;
    }
    #btn_3 {
      background: #feef33;
      border-bottom-left-radius: 154px;
    }
    #btn_4 {
      background: #bede15;
      border-bottom-right-radius: 154px;
    }
  }
}
@media screen and (max-width: 800px) {
  .simon {
    flex-direction: column;
    .container {
      margin-bottom: 10px;
      flex-direction: row !important;
    }
  }
}
</style>
