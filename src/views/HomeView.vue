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
    <div class="sidebar_wrapper">
      <div class="me_pic-placeholder">
        <img
          alt="pic of me in a cafe"
          class="me_pic test"
          src="../assets/pics/meNormal.jpg"
        />
      </div>
      <div>
        <img
          alt="pic of me as a coder"
          class="me_pic"
          src="../assets/pics/meTech.png"
        />
      </div>
      <div>
        <img
          alt="pic of me as a coder"
          class="me_pic"
          src="../assets/pics/meTech.jpg"
        />
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "HomeView",
  components: {},
  data() {
    return {
      scrollFactor: 0,
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
  },
  created() {
    window.addEventListener("scroll", this.handleScroll);
  },
};
</script>

<style>
.home {
  height: 300vh;
  --scroll-factor: 1;
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

.sidebar_wrapper {
  display: flex;
  flex-direction: column;
  position: sticky;
  top: 0vh;
  margin-top: calc(-100vh * var(--scroll-factor));
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
</style>
