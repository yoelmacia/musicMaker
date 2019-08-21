<template>
  <div id="app">
    <div class="Title">Music Maker</div>
    <div class="Profile">
      <button>List Songs</button>
      <div>Artist Picture</div>
      <div>Artist Name</div>
    </div>
    <div class="Gallery">Gallery</div>
  </div>
</template>

<script>
export default {
  name: "app",
  components: {}
};
</script>

<style>
body {
  background-color: black;
  color: #fff;
}
#app {
  text-align: center;
  padding: 5%;
}
.Title {
  font-size: 30px;
}
</style>
