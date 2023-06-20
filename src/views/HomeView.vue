<template>
  <main class="home">
    <div id="entry">
      <figure class="entry-wrapper">
        <img
          alt="pic of me inside my laptop"
          id="entry_pic"
          src="../assets/pics/laptop.jpg"
        />
        <figcaption class="entry_pic-cap">
          Welcome {{ scrollFactor }}
        </figcaption>
      </figure>
    </div>
    <div class="home_wrapper">
      <aside class="home_aside">
        <div class="sidebar_wrapper">
          <div class="home_pic">
            <img
              alt="pic of me in a cafe"
              class="me_pic me_pic-placeholder"
              src="../assets/pics/meNormal.jpg"
            />
          </div>
          <div class="home_pic">
            <img
              alt="pic of me as a coder"
              class="me_pic"
              src="../assets/pics/meTech.png"
            />
          </div>
          <div class="home_pic">
            <img
              alt="pic of me as a coder"
              class="me_pic"
              src="../assets/pics/meTech.jpg"
            />
          </div>
        </div>
      </aside>
      <section>
        <h2>Anja Wurlitzer</h2>
        <p>
          bla bla bla Lorem ipsum dolor sit amet consectetur adipisicing elit.
          Laboriosam facilis harum nulla sit officia autem porro impedit dolorum
          veniam beatae non, mollitia provident veritatis totam! Dicta
          repellendus obcaecati saepe exercitationem?
        </p>

        <div class="home_samples">
          <label
            v-for="compName of compNames"
            :key="compName"
            :for="compName"
            class="home_sample-label"
            @click="scrollToElement(compName + '1')"
            :id="compName + '1'"
          >
            <input
              type="radio"
              name="selectSample"
              :id="compName"
              class="home_sample-radio"
              v-model="currentSample"
            />
            <div class="home_sample-wrapper">
              <component :is="compName + 'View'" class="home_sample-sample" />
              <div class="home_sample-close" @click="closeSample">x</div>
            </div>
            <p class="home_sample-descr">{{ compName }}</p>
          </label>
        </div>
      </section>
    </div>
  </main>
</template>

<script>
import TicTacToeView from "./TicTacToeView.vue";
import ColorMixerView from "./ColorMixerView.vue";
import CounterView from "./CounterView.vue";
import PasswordCheckView from "./PasswordCheckView.vue";
import TodoView from "./TodoView.vue";

export default {
  name: "HomeView",
  components: {
    TicTacToeView,
    ColorMixerView,
    CounterView,
    PasswordCheckView,
    TodoView,
  },
  data() {
    return {
      scrollFactor: 0,
      currentSample: false,
      compNames: [
        "TicTacToe",
        "ColorMixer",
        "Counter",
        "PasswordCheck",
        "Todo",
      ],
    };
  },
  methods: {
    getScrollFactor() {
      return (this.scrollFactor =
        (window.innerHeight - window.scrollY) / window.innerHeight);
    },
    handleScroll() {
      this.getScrollFactor();
      const mainEl = document.querySelector(".home");
      const entryPic = document.querySelector("#entry_pic");
      const picExchange = document.querySelector(".me_pic-placeholder");
      let zoomFactor = Math.pow(2 - this.scrollFactor, 2);

      if (this.scrollFactor < 1 && this.scrollFactor > 0.3) {
        // make entry pic smaller when scrolling down
        mainEl.style.setProperty("--scroll-factor", this.scrollFactor);
        entryPic.classList.remove("become-invisible");
        picExchange.classList.add("become-invisible");
        //zoom in when scrolling
        entryPic.style.setProperty("--zoom-factor", zoomFactor);
      } else if (this.scrollFactor <= 0.3 && this.scrollFactor > 0) {
        mainEl.style.setProperty("--scroll-factor", 0.3);
        entryPic.classList.add("become-invisible");
        picExchange.classList.remove("become-invisible");
      }
      //let figcaption disappear
      if (this.scrollFactor < 0.8) {
        document
          .querySelector(".entry_pic-cap")
          .classList.add("become-invisible");
      } else if (this.scrollFactor > 0.8) {
        document
          .querySelector(".entry_pic-cap")
          .classList.remove("become-invisible");
      }
    },
    closeSample() {
      this.currentSample = false;
      // e.target.parentElement.blur();
    },
  },
  created() {
    window.addEventListener("scroll", this.handleScroll);
  },
};
</script>

<style>
.home {
  _height: 300vh;
  --scroll-factor: 1;
}

.home_wrapper {
  display: grid;
  grid-template-columns: 30vw 1fr;
}

#entry {
  width: 100vw;
  height: 100vh;
  overflow: hidden;

  position: relative;
  z-index: 1;

  scale: var(--scroll-factor);
  transform-origin: 0% 100%;
  transition: scale 0.05s linear;
}

#entry_pic {
  width: 100vw;
  height: 100vh;
  object-fit: cover;

  --zoom-factor: 1;
  scale: var(--zoom-factor);
  transform-origin: 30% 30%;

  _transition: opacity 0.2s ease-in;
}

.entry-wrapper {
  position: relative;
  margin: 0;
}

.entry_pic-cap {
  position: absolute;
  top: 50%;
  left: 50%;
  translate: -50% -50%;
  color: white;
  font-size: 4rem;

  opacity: 1;
  transition: opacity 0.4s ease-in;
}

.home_aside {
}

.sidebar_wrapper {
  display: flex;
  flex-direction: column;
  position: sticky;
  top: 0vh;
  margin-top: calc(-100vh * var(--scroll-factor));
}

.home_pic {
  width: fit-content;
}

.me_pic {
  height: 30vh;
  aspect-ratio: 3/4;
  object-fit: cover;
  object-position: 50% 0%;
  _margin-block: 5vh;
}

.me_pic-placeholder {
  height: calc(100vh * var(--scroll-factor));
  opacity: 1;
  transition: opacity 0.3s ease-out;
}

.become-invisible {
  opacity: 0;
}

.home_samples {
  position: relative;
  display: flex;
  flex-wrap: wrap;
  _justify-content: space-around;
  _gap: 4vmax;

  padding-block: 7rem;
}

.home_sample-label {
  border: 2px solid black;
  border-radius: 10%;
  transform-origin: bottom right;
  transform: rotate3d(-1, -1, 0.2, 30deg);
  _transform-style: preserve-3d;
  transition: transform 0.4s ease-in-out;
  cursor: pointer;
}

.home_sample-label:has(> .home_sample-radio:checked) {
  transform: rotate3d(0, 0, 0, 0deg);
  cursor: auto;
}

.home_sample-descr {
  color: black;
  text-align: center;
}

.home_sample-wrapper {
  width: 10vw;
  max-width: 500px;
  height: 10vw;
  border-radius: 100%;
  overflow: hidden;
  margin: 1rem 2rem;
  position: relative;
}

/*for media devices supoorting hover (no touch) -> :hover state can stick as triggered*/
@media (hover: hover) {
  .home_sample-label:hover {
    transform: rotate3d(0, -0.5, 0, 25deg) scale(1);
  }
}

.home_sample-sample {
  transform-origin: -5% 0%;

  width: 100vw;
  max-width: 1250px;
  min-height: fit-content;
  scale: 0.2;
  opacity: 0.8;
  filter: grayscale(0.6);
  transition: opacity 0.5s ease-in-out;
  pointer-events: none;
}

.home_sample-wrapper:hover > .home_sample-sample {
  opacity: 1;
  filter: grayscale(0);
}

.home_sample-radio {
  display: none;
}

.home_sample-radio:checked ~ .home_sample-wrapper {
  width: 70vw;
  width: max-content;
  height: 70vh;
  border-radius: 0%;
  _overflow: visible;
}

.home_sample-radio:checked ~ .home_sample-wrapper > .home_sample-sample {
  _overflow: auto;
  scale: 0.7;
  opacity: 1;
  pointer-events: all;
  _box-shadow: 2rem 1rem 5rem 0rem;
  _max-width: 100vw;
}

.home_sample-close {
  display: none;
}
.home_sample-radio:checked ~ .home_sample-wrapper > .home_sample-close {
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
