<template>
  <body class="clock_body">
    <div id="clock">
      <div id="center"></div>
      <div class="pointer" id="hourpointer"></div>
      <div class="pointer" id="minpointer"></div>
      <div class="pointer" id="secpointer"></div>
    </div>
    <p class="clock_p">{{ localTime }}</p>
  </body>
</template>

<script>
export default {
  data() {
    return {
      h: new Date().getHours(),
      min: new Date().getMinutes(),
      s: new Date().getSeconds(),
      localTime: " ",
    };
  },
  created() {
    setInterval(() => {
      this.localTime = new Date();
    }, 1000);
  },
};
</script>

<style>
.clock_body {
  font-size: 36px;
  font-family: monospace;
  background-color: gold;
  height: 100vh;
  display: grid;
  align-content: center;
  justify-items: center;
  margin-top: 0.5rem;
}

#clock {
  width: 40vmin;
  height: 40vmin;
  background-color: white;
  border-radius: 100%;
  outline: 3px solid black;
  box-shadow: 2px 2px 5px #333;
  position: relative;
}

.clock_p {
  margin-top: 1rem;
}

#center {
  width: 2vmin;
  height: 2vmin;
  background-color: black;
  border-radius: 100%;
  position: relative;
  left: 50%;
  top: 50%;
  translate: -50%-50%;
}

.pointer {
  width: 1vmin;
  height: 48%;
  background-color: black;
  border-radius: 100px 100px;
  position: relative;
  left: 50%;
  translate: -50%;
  transform-origin: bottom;
}
#hourpointer {
  height: 25%;
  top: 20%;
}

#minpointer {
  top: -28%;
}

#secpointer {
  width: 0.5vmin;
  top: -76%;
}
</style>
