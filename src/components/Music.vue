<template>
  <div>
    <header>Top songs</header>
    <div v-for="song in songs" v-bind:key="song.name">
      <div :style="'background-image:url(http://direct.rhapsody.com/imageserver/v2/albums/' + song.albumId + '/images/300x300.jpg); left: 1%'" class="cover">
        <div class="content-name">{{song.name}}</div>
        <div style="bottom: 0">
        <audio controls class="audio">
        <source :src="song.previewURL" type="audio/mpeg">
      </audio>
      </div>

      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Music',
  props: {
  },
  data: function () {
    return {
      songs: null
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      axios.get('https://api.napster.com/v2.1/tracks/top?apikey=').then((res) => {
        console.log(res)
        this.songs = res.data.tracks
      })
      .catch((error) => {
        console.error(error)
      })
    },

  }
}
</script>

<style>
header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #fff;
}
.track-cover {
  background-size: cover;
  width: 300px;
  height: 300px;
  display: inline-block;
}

.cover {
  background-size: cover;
  width: 300px;
  height: 300px;
  display: inline-block;
  margin: 10px;
  float: left;
  border: 3px solid black; 
  position: relative;
}

.cover:hover {
  cursor: pointer;
}

.audio {
    position: absolute;
    bottom: 0;
}

.content-name{
  color: white;
  font-size: 25px;
  text-align: center;
  text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black;
}

</style>
