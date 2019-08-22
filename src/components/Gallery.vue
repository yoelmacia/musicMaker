<template>
  <div>
    <div
      @click="playSong(item.music_file_path)"
      class="gallery"
      v-for="(item, index) in songs"
      :key="index"
    >
      <img :src="item.cover_image_path" class="gallery-image" />
      <p class="gallery-name">{{ item.name }}</p>
      <div class="track-play">
        <div class="track-inner">
          <div v-if="url === item.music_file_path">||</div>
          <div v-else>&#9654;</div>
        </div>
      </div>
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
  bottom: 0;
}
.track-play {
  width: 250px;
  height: 250px;
}

.track-inner {
  position: absolute;
  text-align: center;
  font-size: 25px;
  background-color: black;
  border-radius: 30px;
  width: 60px;
  height: 60px;
  color: white;
  padding-top: 13px;
  margin-left: 95px;
  margin-top: 95px;
  opacity: 0;
}

.track-inner:hover {
  opacity: 0.8;
  animation-name: fade-in;
  animation-duration: 0.5ms;
}

@keyframes fade-in {
  from {
    opacity: 0;
  }
  to {
    opacity: 0.8;
  }
}
</style>