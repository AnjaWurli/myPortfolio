<template>
  <div class="about">
    <div class="about_pic-wrapper scroll-stop">
      <div class="about_pic-turner">
        <div class="about_pic"></div>
        <div class="about_pic-other"></div>
      </div>
    </div>
    <div class="about_main">
      <section class="about_section-wrapper">
        <div class="about_section">
          <h2>About me</h2>
          <em>28 Jahre / Leipzig / Junior Front End Developer</em>
          <p>
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ad aliquam
            quos voluptatum voluptate nostrum doloremque mollitia enim incidunt
            eaque dolore repudiandae quam obcaecati, non commodi corrupti harum
            veniam alias autem.
          </p>
        </div>
      </section>

      <section class="about_section-wrapper">
        <div class="about_section">
          <h2>Skills</h2>
          <div class="about_section-inner">
            <h3>Hard</h3>
            <ul class="about_ul">
              <li>HTML</li>
              <li>CSS</li>
              <li>JavaScript</li>
              <li>Vue 3</li>
              <li>Git</li>
              <li>Cypress</li>
              <li>Jest</li>
              <li>NPM</li>
              <li>Node</li>
              <li>VS Code</li>
              <li>REST API</li>
            </ul>
          </div>
          <div class="about_section-inner">
            <h3>Soft</h3>
            <ul class="about_ul">
              <li>Kommunikation</li>
              <li>Problemlösung</li>
              <li>Scrum</li>
              <li>Teamfähigkeit</li>
              <li>Selbstreflexion</li>
              <li>Improvisationstalent</li>
            </ul>
          </div>
        </div>
      </section>
      <section class="about_section-wrapper about_section-small">
        <div class="about_section">
          <h2>Hobbies</h2>
          <ul class="about_ul">
            <li>Modeln</li>
            <li>Fitness</li>
            <li>Musik</li>
            <li>Jornaling</li>
          </ul>
        </div>
      </section>
      <section class="about_section-wrapper about_section-small">
        <div class="about_section">
          <h2>Sprachen</h2>
          <ul class="about_ul">
            <li>Deutsch <small>Muttersprache</small></li>
            <li>Englisch <small>B2</small></li>
          </ul>
        </div>
      </section>
      <section class="about_section-wrapper about_section-small">
        <div class="about_section">
          <h2>Führerscheine</h2>
          <ul class="about_ul">
            <li>Klasse B <small>2013</small></li>
            <li>Flurmittelförderschein <small>2020</small></li>
          </ul>
        </div>
      </section>
    </div>
    <div class="scroll-stop about_samples">
      <router-view>
        <div class="about_sample-wrapper">
          <div class="about_sample-shadow"></div>
          <tic-tac-toe-view />
        </div>
        <div class="about_sample-wrapper">
          <div class="about_sample-shadow"></div>
          <color-mixer-view />
        </div>
        <div class="about_sample-wrapper">
          <div class="about_sample-shadow"></div>
          <counter-view />
        </div>
        <div class="about_sample-wrapper">
          <div class="about_sample-shadow"></div>
          <password-check-view />
        </div>
        <div class="about_sample-wrapper">
          <div class="about_sample-shadow"></div>
          <todo-view />
        </div>
      </router-view>
    </div>
  </div>
</template>

<script>
import TicTacToeView from "./TicTacToeView.vue";
import ColorMixerView from "./ColorMixerView.vue";
import CounterView from "./CounterView.vue";
import PasswordCheckView from "./PasswordCheckView.vue";
import TodoView from "./TodoView.vue";
export default {
  components: {
    TicTacToeView,
    ColorMixerView,
    CounterView,
    PasswordCheckView,
    TodoView,
  },
};
</script>

<style>
.about {
  display: grid;
  grid-template-columns: 35vw 65vw;
  grid-template-rows: 1fr 1fr;
  row-gap: 1rem;

  height: 100vh;
  overflow: scroll;
  scroll-snap-type: y mandatory;
  scroll-padding: 2.5vh;
}

.scroll-stop {
  scroll-snap-stop: always;
  scroll-snap-align: start;
}

.about_pic-wrapper {
  position: relative;
  width: 30vw;
  margin-left: 5vw;
  margin-top: 2.5vh;
}

.about_pic-turner {
  box-shadow: 0px 0px 20px black;
  background: radial-gradient(
    circle,
    rgba(13, 13, 13, 1) 42%,
    rgba(38, 38, 38, 1) 89%,
    rgba(65, 65, 65, 1) 100%
  );
  /*radial-gradient(
        rgba(255, 255, 255, 0) 0,
        rgba(255, 255, 255, 0.15) 30%,
        rgba(255, 255, 255, 0.3) 32%,
        rgba(255, 255, 255, 0) 33%
      )
      5rem -5rem,
    radial-gradient(
        rgba(255, 255, 255, 0) 0,
        rgba(255, 255, 255, 0.2) 17%,
        rgba(255, 255, 255, 0.43) 19%,
        rgba(255, 255, 255, 0) 20%
      )
      10rem 3rem,
  background-repeat: no-repeat;
  background-size: 470px 470px, 410px 410px, 100% 100%;*/
  _border-radius: 2rem;
  transition: transform 0.6s;
  transform-style: preserve-3d;
}

.about_pic,
.about_pic-other {
  background-image: url("../assets/me1.png");
  width: 30vw;
  height: 95vh;
  background-size: cover;
  background-repeat: no-repeat;
  _background-position: 0% 0%;
  backface-visibility: hidden;
}

.about_pic-other {
  background-image: url("../assets/me2.png");
  position: absolute;
  top: 0;
  _background-position: 2rem 0;
  transform: rotateY(180deg);
}

.about_pic-wrapper:hover .about_pic-turner {
  transform: rotateY(180deg);
}

.about_main {
  margin: 5vw 2.5vw;
  position: relative;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  align-items: start;
  height: 85vh;
  overflow: scroll;
  scroll-snap-type: y mandatory;
}

.about_main > :not(.about_section-small) {
  grid-column: 1 / span3;
}

.about_main::-webkit-scrollbar {
  _border: 2px solid red;
}

.about_section-wrapper {
  scroll-snap-stop: normal;
  scroll-snap-align: start;
}

.about_section,
.about_section-inner {
  background-color: rgba(130, 130, 130, 0.5);
  padding: 1rem;
  margin: 1rem 0;
  border-radius: 1rem;
  text-align: center;
}

.about_section {
  display: grid;
  grid-template-columns: 50% 50%;
  margin: 20vh 0;
}

.about_section :not(.about_section-inner) {
  grid-column: 1 / span2;
}
.about_section .about_section-inner {
  padding: 0.2rem;
  margin: 0.5rem;
}

.about_ul {
  display: flex;
  flex-wrap: wrap;
  padding: 0;
  justify-content: center;
}

.about_ul li {
  list-style: none;
  background-color: rgba(255, 255, 255, 0.5);
  padding: 0.7rem 1rem;
  margin: 0.3rem 0.5rem;
  border-radius: 0.5rem;
  font-family: "Courier New", Courier, monospace;
}

.about_section-small {
  align-content: start;
  margin: 0.2rem;
}

.about_samples {
  grid-column: 1 / span2;
  position: relative;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.about_sample-wrapper {
  width: 40vmax;
  height: 40vmin;
  margin-top: 1rem;
  border: solid red 2px;
  position: relative;
  transform: rotate3d(-1.5, -1, 0.3, 40deg);
  transform-style: preserve-3d;
}

.about_sample-shadow {
  width: inherit;
  height: inherit;
  background: black;
  opacity: 0.5;
  filter: blur(1rem);
  transform-origin: bottom center;
  transform: rotateX(90deg);
  translate: 0rem 2rem -2rem;
  position: relative;
}

.about_sample-wrapper > :not(.about_sample-shadow) {
  transform-origin: 0% 0%;
  width: 100vmax;
  height: 100vmin;
  scale: 0.4;
  position: absolute;
  top: 0;
  left: 0;
  overflow: hidden;
}
</style>
