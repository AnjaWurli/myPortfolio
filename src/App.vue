<template>
  <body
    id="body_app"
    :class="{ 'lightswitch_body-dark': lightswitchOff }"
    @mousemove="update"
    @touchmove="update"
  >
    <button
      class="lightswitch_button"
      :class="{ 'lightswitch_button-dark': lightswitchOff }"
      @click="lightswitchOff = !lightswitchOff"
    >
      Light
    </button>

    <nav id="main-nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link :to="{ name: 'todo' }">Todo-App</router-link> |
      <router-link :to="{ name: 'tictactoe' }">TicTacToe</router-link>
      <router-link :to="{ name: 'colormixer' }">Color-Mixer</router-link> |
      <router-link :to="{ name: 'counter' }">Counter</router-link> |
      <router-link :to="{ name: 'passwordcheck' }">Password-Check</router-link>
      |
      <router-link :to="{ name: 'clock' }">Clock</router-link>
    </nav>

    <router-view />
  </body>
</template>

<style>
html {
  box-sizing: border-box;
  --background-color: #f5f5f5;
  --text-color: #333;

  --cursorX: 50vw;
  --cursorY: 50vh;
  _background-color: var(--background-color);
}
body {
  /*bezieht sich auf die View */
  margin: 0;
  padding: 0;
}
#main-nav {
  margin-left: 15vmin;
  padding: 30px;
  text-align: center;
}

#main-nav a {
  font-weight: bold;
  color: var(--text-color);
}

#main-nav a.router-link-exact-active {
  color: #42b983;
}

#body_app {
  background-color: var(--background-color);
  color: var(--text-color);
  transition: background 1s ease-in-out;
  _padding-inline: 1rem;
  min-height: 100vh;
  max-height: fit-content;

  /*cursor beleuchtung */
  _background: radial-gradient(
    circle 10vmax at var(--cursorX) var(--cursorY),
    rgba(233, 240, 20, 0.638) 0%,
    var(--background-color)
  );
}
.lightswitch_body-dark {
  --background-color: #333;
  --text-color: snow;
}

.lightswitch_button {
  background-color: var(--background-color);
  color: var(--text-color);
  _font-size: 2rem;
  font-family: monospace;
  padding: 0.5rem 1rem;
  border: 5px solid var(--text-color);
  border-radius: 2px;
  cursor: pointer;
  position: absolute;
  top: 1.5rem;
  left: 1.5rem;
  width: 18vmin;
  height: fit-content;
}

@media screen and (max-width: 450px) {
  .lightswitch_button {
    padding: 0.2rem;
  }
}

.lightswitch_button-dark {
  box-shadow: 0 0 5px yellow, 0 0 10px yellow, 0 0 20px yellow;
}
</style>

<script>
export default {
  data() {
    return {
      lightswitchOff: false,
    };
  },
  methods: {
    update(e) {
      let x = e.clientX || e.touches[0].clientX;
      let y = e.clientY || e.touches[0].clientY;

      document.documentElement.style.setProperty("--cursorX", x + "px");
      document.documentElement.style.setProperty("--cursorY", y + "px");
    },
  },
};
</script>
