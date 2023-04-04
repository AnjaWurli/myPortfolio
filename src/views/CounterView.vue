<template>
  <div class="counter_body">
    <header :style="{ '--color': color }" class="counter_header">
      <section>
        <h1>Counter</h1>
        <p class="counter_p">
          (click the white area or hit space / enter to count)
        </p>
      </section>
      <section class="counter_inputWrapper">
        <div class="counter_rangeWrapper">
          <label for="increaseBy">increase by: {{ increaseBy }}</label>
          <input
            id="increaseBy"
            type="range"
            min="1"
            max="20"
            v-model.number="increaseBy"
            class="counter_range"
          />
        </div>
        <button @click="reset" class="counter_button">Reset</button>
      </section>
    </header>
    <main
      @click="increaseCounter"
      :style="{ '--counter': counter - hundred + '%', '--color': color }"
      class="counter_main"
    >
      <div id="counter">{{ counter }}</div>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      counter: 0,
      hundred: 0,
      color: "",
      increaseBy: 10,
    };
  },
  methods: {
    increaseCounter() {
      this.counter += this.increaseBy;
      if (this.counter - this.hundred > 100) {
        this.hundred += 100;
        this.color = this.randomColor();
      }
    },
    countKey(event) {
      //only with space or enter
      if (event.code === "Enter" || event.code === "Space") {
        this.increaseCounter();
      }
    },
    reset(e) {
      this.counter = 0;
      this.hundred = 0;
      this.color = "";
      e.target.blur();
    },
    random(min, max) {
      const num = Math.floor(Math.random() * (max - min)) + min;
      return num;
    },
    randomColor() {
      return `rgb(${this.random(0, 255)}, ${this.random(0, 255)}, ${this.random(
        0,
        255
      )})`;
    },
  },
  created() {
    window.addEventListener("keydown", this.countKey);
  },
};
</script>

<style>
.counter_body {
  font-size: 16px;
  font-family: monospace;
  --color: gold;

  height: 100vh;
  display: grid;
  grid-template-rows: auto 1fr;
}

.counter_header {
  background-color: var(--color);
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  padding: 1.5rem;
  font-size: 2rem;
}

.counter_inputWrapper {
  flex-grow: 2;
  display: flex;
  justify-content: space-evenly;
}

.counter_p {
  font-size: 1.25rem;
}
.counter_button {
  cursor: pointer;
  background-color: white;
  border: 2px solid black;
  box-shadow: 3px 3px 0 white;
  font-size: 1.5rem;
  margin: 1rem 0.5rem;
  height: 2.5rem;
  width: 6rem;
}

.counter_button:active {
  box-shadow: none;
}

.counter_main {
  background-image: linear-gradient(
    90deg,
    var(--color) var(--counter),
    transparent 0
  );
  display: grid;
  place-content: center;
}

#counter {
  font-size: 5rem;
}

.counter_rangeWrapper {
  font-size: 1rem;
  display: grid;
  padding-block: 1rem;
}
.counter_range {
  accent-color: black;
}
</style>
