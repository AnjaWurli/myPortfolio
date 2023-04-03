<template>
  <body>
    <main class="ttt-body">
      <h1 class="ttt-h1">{{ gamer }}</h1>

      <div
        v-for="n in 9"
        :key="n"
        class="ttt-square"
        :id="'s' + n"
        @click="set"
      ></div>

      <button class="ttt-button" @click="reset">New Game</button>
      <div class="ttt-box"></div>
    </main>
  </body>
</template>

<script>
export default {
  data() {
    return {
      gamer: "Player 1",
      circled: [],
      crossed: [],
      counter: 0,
    };
  },
  methods: {
    log(e) {
      console.log(e);
    },
    win(result, winner) {
      const test = [
        [1, 2, 3],
        [4, 5, 6],
        [7, 8, 9],
        [1, 4, 7],
        [2, 5, 8],
        [3, 6, 9],
        [1, 5, 9],
        [3, 5, 7],
      ];

      for (let num of test) {
        const [x, y, z] = num;
        if (
          result.includes("s" + x) &&
          result.includes("s" + y) &&
          result.includes("s" + z)
        ) {
          this.gamer = winner + " won!";
          document.querySelector(`#s${x}`).classList.add("winner");
          document.querySelector(`#s${y}`).classList.add("winner");
          document.querySelector(`#s${z}`).classList.add("winner");

          document
            .querySelector(".ttt-box")
            .style.setProperty("pointer-events", "all");
        } else if (this.counter === 9) {
          this.gamer = "Draw!";
        }
      }
    },
    set(e) {
      if (!e.target.innerHTML) {
        this.counter++;
        if (this.gamer === "Player 1") {
          e.target.innerHTML =
            '<span class="circle ttt-span" style="color:#5F9EA0;pointer-events:none">&#9900;</span>';
          this.gamer = "Player 2";
        } else {
          e.target.innerHTML =
            '<span class="cross ttt-span" style="color:#DC143C;pointer-events:none">&#215;</span>';
          this.gamer = "Player 1";
        }
        if (e.target.firstElementChild.className.split(" ")[0] === "circle") {
          this.circled.push(e.target.id);
        } else if (
          e.target.firstElementChild.className.split(" ")[0] === "cross"
        ) {
          this.crossed.push(e.target.id);
        }
      }
      //results
      if (this.counter >= 5) {
        this.win(this.circled, "Player 1");
        this.win(this.crossed, "Player 2");
      }
    },
    reset() {
      document.querySelectorAll(".ttt-span").forEach((symbol) => {
        symbol.remove();
      });
      this.gamer = "Player 1";
      this.crossed = [];
      this.circled = [];
      this.counter = 0;

      document.querySelectorAll(".ttt-square").forEach((el) => {
        el.classList.remove("winner");
      });
      document
        .querySelector(".ttt-box")
        .style.setProperty("pointer-events", "none");
    },
  },
};
</script>
<style>
.ttt-body {
  --bg-color: #072931;
  --border-color: #0d404c;
  --hover-color: #1c3a40;
  background-color: var(--bg-color);
  color: white;
  font-family: sans-serif;
  margin: 0;

  display: grid;
  grid-template-columns: repeat(3, 20vmin);
  justify-content: center;
  align-content: center;
  position: relative;
}

.ttt-h1 {
  grid-column: span 3;
  justify-self: center;
  align-self: start;
  font-weight: 400;
  font-size: 5vmin;
}

.ttt-button {
  grid-column: span 3;
  justify-self: center;
  margin: 2rem;
  align-self: end;
  border: 3px solid var(--border-color);
  border-radius: 7px;
  font-size: 2vmin;
  color: white;
  background-color: var(--bg-color);
  padding: 0.5rem 1rem;
  cursor: pointer;
}

.ttt-square {
  aspect-ratio: 1/1;
  border: 0.3vmin solid var(--border-color);
  transition: background-color 0.5s;
  text-align: center;
  cursor: pointer;
}

.ttt-square:hover,
.ttt-button:hover {
  background-color: var(--hover-color);
}

.ttt-box {
  position: absolute;
  outline: 4vmin solid var(--bg-color);
  width: 58vmin;
  height: 58vmin;
  top: 15vmin;
  left: 50%;
  translate: -50% -1.5vmin;
  pointer-events: none;
}
.ttt-span {
  font-size: 15vmin;
  display: block;
}
.circle {
  scale: 2;
  translate: 0 -13%;
}

.winner {
  background-color: var(--hover-color);
  pointer-events: none;
}
.winner .ttt-span {
  scale: 2;
  translate: 0 -13%;
  transition: scale 1s;
}
.winner .circle {
  scale: 3;
  translate: 0 -22%;
  transition: scale 1s;
}
</style>
