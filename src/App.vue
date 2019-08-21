<template>
  <div id="app">
    <div class="Title">Music Maker</div>
    <div class="Profile">
      <button @click="getData()">List Songs</button>
      <div>Artist Picture</div>
      <div>Artist Name</div>
    </div>
    <div class="Gallery">Gallery</div>
  </div>
</template>

<script>
const BASEURL = "https://api-stg.jam-community.com/song/trending";
import songs from "./assets/songs.json";
export default {
  name: "app",
  components: {},
  data() {
    return {
      songs: null
    };
  },
  methods: {
    receiveData() {
      fetch(BASEURL, {
        method: "GET",
        mode: "cors",
        headers: {
          "Content-Type": "application/x-www-form-urlencoded"
        }
      }).then(response => {
        // JSON responses are automatically parsed.
        this.songs = response.data;
        console.log(response);
      });
    },
    getData() {
      this.songs = songs;
    }
  }
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
