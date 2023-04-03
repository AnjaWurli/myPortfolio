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
              <li v-for="hardSkill of skills.hard" :key="hardSkill">
                {{ hardSkill }}
              </li>
            </ul>
          </div>
          <div class="about_section-inner">
            <h3>Soft</h3>
            <ul class="about_ul">
              <li v-for="softSkill of skills.soft" :key="softSkill">
                {{ softSkill }}
              </li>
            </ul>
          </div>
        </div>
      </section>
      <section class="about_section-wrapper about_section-small">
        <div class="about_section">
          <h2>Hobbies</h2>
          <ul class="about_ul">
            <li v-for="hobby of hobbies" :key="hobby">
              {{ hobby }}
            </li>
          </ul>
        </div>
      </section>
      <section class="about_section-wrapper about_section-small">
        <div class="about_section">
          <h2>Sprachen</h2>
          <ul class="about_ul">
            <li v-for="(level, language) in languages" :key="language">
              {{ language }} <small>{{ level }}</small>
            </li>
          </ul>
        </div>
      </section>
      <section class="about_section-wrapper about_section-small">
        <div class="about_section">
          <h2>Führerscheine</h2>
          <ul class="about_ul">
            <li v-for="(year, licence) in licences" :key="licence">
              {{ licence }} <small>{{ year }}</small>
            </li>
          </ul>
        </div>
      </section>
    </div>
    <div class="scroll-stop2 about_samples">
      <label
        v-for="compName of compNames"
        :key="compName"
        :for="compName"
        class="about_sample-label"
        @click="scrollToElement(compName + '1')"
        :id="compName + '1'"
      >
        <input
          type="radio"
          name="selectSample"
          :id="compName"
          class="about_sample-radio"
          v-model="currentSample"
        />
        <div class="about_sample-wrapper">
          <div class="about_sample-shadow"></div>
          <component :is="compName" class="about_sample-sample" />
          <div class="about_sample-close" @click="currentSample = false">x</div>
        </div>
      </label>
    </div>
  </div>
</template>

<script>
import TicTacToeView from "./TicTacToeView.vue";
import ColorMixerView from "./ColorMixerView.vue";
import CounterView from "./CounterView.vue";
import PasswordCheckView from "./PasswordCheckView.vue";
import TodoView from "./TodoView.vue";

import { ref } from "vue";

export default {
  components: {
    TicTacToeView,
    ColorMixerView,
    CounterView,
    PasswordCheckView,
    TodoView,
  },
  data() {
    return {
      skills: {
        hard: [
          "HTML",
          "CSS",
          "JavaScript",
          "Vue 3",
          "Git",
          "Cypress",
          "Jest",
          "NPM",
          "Node",
          "VS Code",
          "REST API",
        ],
        soft: [
          "Kommunikation",
          "Problemlösung",
          "Scrum",
          "Teamfähigkeit",
          "Selbstreflexion",
          "Improvisationstalent",
        ],
      },
      hobbies: ["Modeln", "Fitness", "Musik", "Jornaling"],
      languages: {
        Deutsch: "Muttersprache",
        Englisch: "B2",
      },
      licences: {
        "Klasse B": "2013",
        Flurmittelförderschein: "2020",
      },
      currentSample: false,
      compNames: [
        "TicTacToeView",
        "ColorMixerView",
        "CounterView",
        "PasswordCheckView",
        "TodoView",
      ],
    };
  },
  methods: {
    scrollToElement(elId) {
      if (this.currentSample) {
        const el = document.getElementById(ref(elId).value);
        el.scrollIntoView();
        console.log(document.getElementById(ref(elId).value));
      }
    },
  },
};
</script>

<style>
.about {
  display: grid;
  grid-template-columns: 35vw 65vw;
  grid-template-rows: 1fr 3fr;
  row-gap: 5rem;

  height: 100vh;
  overflow: scroll;
  scroll-snap-type: y mandatory;
}

.scroll-stop {
  scroll-snap-stop: normal;
  scroll-snap-align: end;
}
.scroll-stop2 {
  scroll-snap-stop: normal;
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
  margin: 2.5vw 2.5vw;
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
  scroll-snap-align: center;
  margin-top: 100vh;
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
  margin-inline: 0.2rem;
}

.about_samples {
  grid-column: 1 / span2;
  position: relative;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;

  height: 100vh;
  overflow: scroll;
  padding-block: 5rem;
}

.about_sample-label {
  margin: 2rem;
}

.about_sample-wrapper {
  width: 40vmax;
  height: 40vmin;
  position: relative;
  transform-origin: center right;
  transform: rotate3d(-1.5, -1, 0.3, 40deg);
  transform-style: preserve-3d;
  transition: transform 0.4s ease-in-out;
  cursor: pointer;
}

.about_sample-wrapper:hover {
  transform: rotate3d(-1.5, -1, 0.2, 30deg) scale(1.05);
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

.about_sample-sample {
  transform-origin: 0% 0%;
  max-width: 100vmax;
  min-width: 100vw;
  min-height: fit-content;
  scale: 0.4;
  position: absolute;
  top: 0;
  left: 0;
  overflow: hidden;
  opacity: 0.8;
  transition: opacity 0.5s ease-in-out;
  pointer-events: none;
}

.about_sample-wrapper:hover > .about_sample-sample {
  opacity: 1;
}

.about_sample-radio {
  display: none;
}

.about_sample-radio:checked ~ .about_sample-wrapper {
  transform: rotate3d(0, 0, 0, 0deg);
  width: 70vw;
  height: 70vh;
  margin: 4rem;

  cursor: auto;
}

.about_sample-radio:checked ~ .about_sample-wrapper > .about_sample-sample {
  overflow: auto;
  scale: 0.7;
  opacity: 1;
  pointer-events: all;
  _box-shadow: 2rem 1rem 5rem 0rem;
}

.about_sample-radio:checked ~ .about_sample-wrapper > .about_sample-shadow {
  transform: rotateX(0deg);
  translate: 2rem -1rem 0rem;
  filter: blur(2rem);
}
.about_sample-close {
  display: none;
}
.about_sample-radio:checked ~ .about_sample-wrapper > .about_sample-close {
  display: block;
  color: white;
  background-color: black;
  opacity: 0.8;
  font-size: 2rem;
  padding: 0.5rem 1rem;
  outline: 2px solid white;
  border-radius: 100%;
  position: absolute;
  top: -1rem;
  right: -1rem;
  cursor: pointer;
}
</style>
