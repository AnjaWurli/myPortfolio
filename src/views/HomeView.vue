<template>
  <main class="home">
    <div id="entry">
      <img
        alt="pic of me inside my laptop"
        id="entry_pic"
        src="../assets/pics/laptop.jpg"
      />
    </div>
    <div id="test"></div>
    <div id="test"></div>
  </main>
</template>

<script>
export default {
  name: "HomeView",
  components: {},
  methods: {
    handleScroll() {
      // besser mit Flexbox?

      const entry = document.querySelector("#entry_pic");
      let entryPos = entry.getBoundingClientRect().top;
      let scrollFactor = 1 - (Math.abs(entryPos) / window.innerHeight) * 4;

      if (scrollFactor < 1 && scrollFactor > 0.3) {
        entry.style.setProperty("--scroll-factor", scrollFactor);
      } else if (scrollFactor <= 0.3 && scrollFactor > 0) {
        entry.style.setProperty("--scroll-factor", 0.3);
      }
    },
  },
  created() {
    window.addEventListener("scroll", this.handleScroll);
  },
};
</script>

<style>
#entry {
  width: 100vw;
  height: 100vh;
}

#entry_pic {
  width: 100vw;
  height: 100vh;
  object-fit: cover;

  --scroll-factor: 1;
  scale: var(--scroll-factor);
  transform-origin: 0% 100%;
  transition: scale 0.05s linear;
}

.home {
  _height: 200vh;
}

#test {
  width: 500px;
  height: 50vh;
  background-color: black;
}
</style>
