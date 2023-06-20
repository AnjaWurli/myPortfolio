<template>
  <body class="tetris">
    <h2>TETRIS</h2>
    <div class="tetris_container">
      <div class="tetris_playground tetris_box">
        <div
          v-for="square of 200"
          class="tetris_playground-square"
          :key="square"
        ></div>
        <div class="tetris_fig"></div>
      </div>
      <div class="tetris_sideInfo">
        <div>Score:</div>
        <div>Level:</div>
        <div class="tetris_sideInfo-moves">
          <p>Rotate</p>
          <p>Move Right</p>
          <p>Move Left</p>
          <p>Move Down</p>
        </div>
        <button>Restart</button>
        <button>Music: Off</button>
      </div>
    </div>
  </body>
</template>

<style>
.tetris {
  background-color: darkslategray;
  color: white;
  height: 80vh;
}

.tetris h2 {
  text-align: center;
}

.tetris_container {
  margin: auto;
  display: flex;
  justify-content: center;
}

.tetris_playground {
  width: 20rem;
  height: 40rem;
  display: grid;
  grid-template: repeat(20, 2rem) / repeat(10, 2rem);
  position: relative;
}

.tetris_playground-square {
  width: 2rem;
  height: 2rem;
  margin: 0;
  border: 0.5px solid rgba(255, 255, 255, 0.2);
  background-color: rgba(255, 255, 255, 0.1);
}

.tetris_box,
.tetris_sideInfo > * {
  border: 2px solid slategray;

  margin: 0.5rem;
}

.tetris_sideInfo > * {
  background-color: transparent;
  color: seashell;
  padding: 1rem;
}

.tetris_sideInfo > button {
  font-family: "Times New Roman", Times, serif;
  font-size: 16px;
}

.tetris_sideInfo > button:hover {
  background-color: slategray;
  color: darkslategray;
}

.tetris_sideInfo-moves p:hover {
  color: yellow;
  cursor: pointer;
}
</style>
