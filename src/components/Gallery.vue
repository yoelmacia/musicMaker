<template>
  <div>
    <div class="gallery" v-for="(item, index) in songs" :key="index">
      <div @click="playSong(item.music_file_path)">
        <img :src="item.cover_image_path" class="gallery-image" />
        <p class="gallery-name">{{ item.name }}</p>
        <div class="track-play">
          <div class="track-inner">
            <div v-if="url === item.music_file_path">||</div>
            <div v-else>&#9654;</div>
          </div>
        </div>
      </div>
      <div>
        <div>Likes: {{ item.likes }}</div>
      </div>
      <div>
        <button @click="likeSong(item.id)">Like</button>
        <button>Comment</button>
      </div>
    </div>
  </div>
</template>

<script>
const LIKEURL =
  "https://api-stg.jam-community.com/interact/like?apikey=___agAFTxkmMIWsmN9zOpM_6l2SkZPPy21LGRlxhYD8";
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
    },
    likeSong(song) {
      fetch(LIKEURL, {
        method: "POST",
        mode: "cors",
        headers: {
          "Access-Control-Allow-Origin": "http://www.jam.dev",
          "Content-Type": "application/x-www-form-urlencoded"
        },
        body: { id: song }
      })
        .then(response => {
          console.log(response);
        })
        .catch(error => {
          console.log(error);
        });
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