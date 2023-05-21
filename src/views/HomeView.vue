<template>
  <div id="entry">
    <img
      alt="pic of me inside my laptop"
      id="entry_pic"
      src="../assets/pics/laptop.jpg"
    />
  </div>
  <div></div>
</template>

<script>
export default {
  name: "HomeView",
  components: {},
};
</script>

<style>
#entry {
  width: 100vw;
  height: 80vh;
}
#entry_pic {
  --pic-size: 100vw;
  vertical-align: top;
  width: var(--pic-size);
  height: calc(var(--pic-size) * 3 / 4);
  _aspect-ratio: 4/3;
}
</style>
