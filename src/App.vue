<template>
<button @click="spotify">test</button>
<div v-for="(song, index) in spotifyData.items" :key="index">
  {{song.track.artists[0].name}}
  {{song.track.name}}
  {{song.track.popularity}}
 </div>
</template>

<script lang="ts">
import { ref } from 'vue'
export default {
  name: 'App',
  setup() {
    let spotifyData = ref<object>(
      {}
    )

    const spotify = () => {
fetch("https://api.spotify.com/v1/me/player/recently-played?=", {
  "method": "GET",
  "headers": {
    "cookie": "sp_m=us; sp_t=c5330428-3561-4253-a486-41cd1e94c728; sp_new=1; sp_landing=https%253A%252F%252Fwww.spotify.com%252Fus%252Faccount%252Foverview%252F; spot=%257B%2522t%2522%253A1614738200%252C%2522m%2522%253A%2522us%2522%252C%2522p%2522%253Anull%257D",
    "Content-Type": "application/json",
    "Authorization": import.meta.env.VITE_API
  }
}).then(res => res.json())
.then(response => {
   console.log(response)
   spotifyData.value = response
})
.catch(err => {
  console.error(err);
});
 
    }

   return {spotify, spotifyData}
  }
}
</script>

<style>
</style>