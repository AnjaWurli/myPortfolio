<template>
  <div class="about">
    <h1>This is an about page</h1>
    <div class="about_pic-wrapper">
      <div class="about_pic me1"></div>
      <div class="about_triangle-wrapper">
        <h2 class="about_h2">Anja Wurlitzer</h2>
      </div>
      <div class="about_pic me2"></div>
    </div>

    <div class="about_info">
      <div class="about_exp">Exp</div>
      <div class="about_contact">Contact</div>
      <div class="about_education">edu</div>
    </div>
    <hr />
  </div>
</template>

<style>
hr {
  width: 90vw;
  height: 0.4rem;
  border: 0;
  box-shadow: inset 1px 10px 1rem -0.5rem rgba(0, 0, 0, 0.5);
}
.about {
  display: grid;
  place-content: center;
}
.about_pic-wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr;
}

.about_pic {
  width: 40vw;
  aspect-ratio: 0.75;
  _border: red 2px solid;
  position: relative;
  z-index: 1;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: 100% 0;
}

.me1 {
  background-image: url("../assets/me1.png");
  background-position: 6vw 0vw;
  justify-self: right;
}

.me2 {
  background-image: url("../assets/me2.png");
}

.about_triangle-wrapper {
  _margin-right: -15vw;
  _margin-left: -20vw;
  position: absolute;
  z-index: 0;
  align-self: end;
  justify-self: center;
  width: 40vw;
  aspect-ratio: 0.5;
  _border: 2px solid purple;
  --triangle: 50%;
  background: linear-gradient(
      var(--background-color) var(--triangle),
      transparent var(--triangle)
    ),
    linear-gradient(
      to left bottom,
      var(--background-color) var(--triangle),
      transparent var(--triangle)
    ),
    linear-gradient(
      to right bottom,
      var(--background-color) var(--triangle),
      purple var(--triangle)
    );
}

.about_h2 {
  position: absolute;
  bottom: 0;
  right: 50%;
  translate: 50%;
  z-index: 1;
  text-align: center;
  color: white;
  margin-bottom: 5vw;
}

.about_info {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}
</style>
