<script setup lang="ts">
import Header from './components/Header.vue'
import Videoplayer from './components/Videoplayer.vue'
import Lock from './components/Lock.vue'
import Checktab from './components/Checktab.vue'
import Fullscreen from './components/Fullscreen.vue'
import RightClickDisable from './components/RightClickDisable.vue'

</script>

<template>
  <Header/>
  <div>
    <Videoplayer videoId="Yg5zkd9nm6w" />
    <Lock/>
    <Checktab/>
    <h1>Note : Browser Restrictions: Modern browsers have strict security policies that require user interaction (e.g., a button click) to initiate fullscreen mode. This prevents websites from unexpectedly entering fullscreen and creating potentially malicious or disruptive experiences.</h1>
    <Fullscreen/>
    <RightClickDisable/>

  </div>
</template>

<style scoped>

</style>
