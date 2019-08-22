<template>
  <div>
    <div class="gallery" v-for="(item, index) in songs" :key="index">
      <img :src="item.cover_image_path" class="gallery-image" />
      <p class="gallery-name">{{ item.name }}</p>
      <button class="gallery-play" @click="playSong(item.music_file_path)">Play</button>
      <button class="gallery-pause" @click="playSong(item.music_file_path)">Pause</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["songs"],
  data: function() {
    return {
      audio: null,
      playing: false,
      url: ""
    };
  },
  methods: {
    playSong(url) {
      let song = new Audio(url);
      if (!this.playing) {
        song.play();
        this.playing = true;
        this.url = url;
        this.audio = song;
      } else {
        if (this.url === url) {
          this.audio.pause();
          this.playing = false;
        } else {
          this.audio.pause();
          song.play();
          this.playing = true;
          this.url = url;
          this.audio = song;
        }
      }
    }
  }
};
</script>

<style>
.gallery {
  display: inline-block;
  width: 250px;
  height: 250px;
  margin: 10px;
  text-align: left;
  cursor: pointer;
  position: relative;
}
.gallery-image {
  width: 250px;
  height: 250px;
  border: 3px solid white;
  position: absolute;
}
.gallery-name {
  width: 250px;
  text-align: center;
  background-color: white;
  color: black;
  position: absolute;
  bottom: 41px;
}
.gallery-play {
  width: 250px;
  text-align: center;
  background-color: white;
  color: black;
  position: absolute;
  bottom: 28px;
}
.gallery-pause {
  width: 250px;
  text-align: center;
  background-color: white;
  color: black;
  position: absolute;
  bottom: 0;
}
</style>