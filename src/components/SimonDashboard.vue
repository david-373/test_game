<template>
  <div class="dashboard" data-v-f3f3eg9>
    <h2>{{ $parent.message }}</h2>
    <div>
      <div style="display: flex; width: 300px">
        <div class="level">
          <h3>Уровень:</h3>
          <div>
            <label for="first">Легкий</label>
            <input
              id="first"
              type="radio"
              name="interval"
              value="1500"
              v-model="$parent.interval"
            />
          </div>
          <div>
            <label for="second">Средний</label>
            <input
              id="second"
              type="radio"
              name="interval"
              value="1000"
              v-model="$parent.interval"
            />
          </div>
          <div>
            <label for="last">Сложный</label>
            <input
              id="last"
              type="radio"
              name="interval"
              value="400"
              v-model="$parent.interval"
            />
          </div>
        </div>
        <h2>
          Раунд
          {{ $parent.clicksCount }}
        </h2>
      </div>
      <button :disabled="$parent.started" @click="$parent.generateClicks()">
        Начать
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
};
</script>

<style lang="scss"  scoped>
.dashboard {
  background: linear-gradient(90deg, #fff 8px, transparent 1%) 95px 100px,
    linear-gradient(#fff 8px, transparent 1%), #ddd;
  background-size: 10px 10px;
  display: flex;
  width: 350px;
  min-width: 350px;
  min-height: 350px;
  flex-flow: column wrap;
  align-items: center;
  border-radius: 20px;
  margin: 0 auto;
  box-shadow: 2px 1px 12px #aaa;
  div {
    h2 {
      width: 50%;
      line-height: 120px;
    }
    .level {
      width: 50%;
    }
    button {
      width: 100px;
      height: 100px;
      border: none;
      border-radius: 50%;
      background: burlywood;
      box-shadow: rgba(0, 0, 0, 0.19) 0px 10px 20px,
        rgba(0, 0, 0, 0.23) 0px 6px 6px;
      color: #fff;
      font-size: 16px;
      &:active {
        box-shadow: rgba(50, 50, 93, 0.25) 0px 30px 60px -12px inset,
          rgba(0, 0, 0, 0.3) 0px 18px 36px -2px inset;
      }
    }
  }
}
</style>