<template>
  <div class="colormixer-wrapper" :style="'background-color: ' + rgbToHex">
    <header class="colormixer-header">
      <nav class="colormixer-nav">
        <form class="colormixer-form">
          <label for="red">r</label>
          <input type="range" step="1" min="0" max="255" id="red" v-model="r" />
        </form>
        <form>
          <label for="green">g</label>
          <input
            type="range"
            step="1"
            min="0"
            max="255"
            id="green"
            v-model="g"
          />
        </form>
        <form>
          <label for="blue">b</label>
          <input
            type="range"
            step="1"
            min="0"
            max="255"
            id="blue"
            v-model="b"
          />
        </form>
        <div>
          <button class="colormixer-button" @click="randomColor">
            Random Color
          </button>
          <span v-show="loading" class="rotate-center">&#10061;</span>
        </div>
      </nav>
      <p>{{ rgbToHex }}</p>
    </header>
  </div>
</template>

<script>
export default {
  data() {
    return {
      r: 255,
      g: 150,
      b: 180,
      loading: false,
    };
  },
  computed: {
    rgbToHex() {
      return "#" + this.hexa(this.r) + this.hexa(this.g) + this.hexa(this.b);
    },
  },
  methods: {
    hexa(n) {
      if (n > 15) {
        return Number(n).toString(16);
      } else {
        return "0" + Number(n).toString(16);
      }
    },
    async randomColor() {
      this.loading = true;
      const response = await fetch("https://dummy-apis.netlify.app/api/color");
      const data = await response.json();

      this.r = data.rgb.r;
      this.g = data.rgb.g;
      this.b = data.rgb.b;

      this.loading = false;
    },
  },
};
</script>
<style>
.colormixer-wrapper {
  height: 85vh;
  font-family: monospace;
  color: black;
  container-type: inline-size;
}

.colormixer-header {
  font-size: 2rem;
  background-color: rgba(255, 255, 255, 0.75);
  padding: 2rem 1rem;
  display: flex;
  justify-content: space-between;
}

.colormixer-nav {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 1rem;
}

@container (max-width: 800px) {
  .colormixer-nav {
    display: flex;
    flex-direction: column;
    align-items: baseline;
  }
}

.colormixer-form {
  display: inline;
}

.colormixer-form + .colormixer-form {
  margin-left: 0.5rem;
}

#red {
  accent-color: red;
}

#green {
  accent-color: green;
}

#blue {
  accent-color: blue;
}

.colormixer-button {
  cursor: pointer;
  background-color: white;
  border: 2px solid black;
  box-shadow: 3px 3px 0 white;
  font-size: 1.5rem;
  width: 7rem;
  font-family: monospace;
}
.colormixer-button:active {
  border-color: dodgerblue;
}

@keyframes rotate-center {
  0% {
    transform: rotate(0);
  }
  100% {
    transform: rotate(360deg);
  }
}
.rotate-center {
  animation: rotate-center 0.4s ease-in-out infinite both;
  display: inline-block;
  translate: 50% 45%;
  opacity: 0.5;
}
</style>
