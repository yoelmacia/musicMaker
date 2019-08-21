<template>
  <div>
    <div class="profile" v-for="(item, index) in songs" :key="index">
      <div>
        <img :src="item.artist.profile_image_path" class="profile-image" />
      </div>
      <div class="profile-info">
        <div class="profile-artist-name">Artist: {{ item.artist.artist_name }}</div>
        <div class="profile-artist-followers">Followers: {{ item.artist.followers }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["songs"]
};
</script>

<style>
.profile {
  display: flex;
  justify-content: center;
}
.profile-image {
  width: 200px;
  height: 200px;
  border: 3px solid white;
  border-radius: 100px;
  object-fit: cover;
}

.profile-info {
  margin-left: 15px;
  align-content: left;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.profile-artist-followers {
  font-size: 20px;
}

.profile-artist-name {
  font-size: 20px;
}
</style>