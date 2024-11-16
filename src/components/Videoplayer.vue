<template>
  <div class="youtube-player">
    <div ref="videoPlayer" class="video-container">
      <iframe
        :src="videoSrc"
        frameborder="0"
        allow="autoplay; encrypted-media"
        allowfullscreen
        class="video-frame"
      ></iframe>
    </div>
    <div class="controls">
      <button @click="playVideo">Play</button>
      <button @click="pauseVideo">Pause</button>
      <button @click="stopVideo">Stop</button>
      <button @click="toggleMute">{{ isMuted ? 'Unmute' : 'Mute' }}</button>
      <input type="range" min="0" max="100" @input="setVolume" v-model="volume" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      player: null,
      isMuted: false,
      volume: 50,
      isPlaying: false,
    };
  },
  props: {
    videoId: {
      type: String,
      required: true,
    },
  },
  computed: {
    videoSrc() {
      return `https://www.youtube.com/embed/${this.videoId}?enablejsapi=1&controls=0&rel=0&modestbranding=1&iv_load_policy=3`;
    },
  },
  mounted() {
    // Load the YouTube IFrame API script if it's not already loaded
    if (!window.YT) {
      const tag = document.createElement("script");
      tag.src = "https://www.youtube.com/iframe_api";
      const firstScriptTag = document.getElementsByTagName("script")[0];
      firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
      window.onYouTubeIframeAPIReady = this.initPlayer;
    } else {
      this.initPlayer();
    }
  },
  methods: {
    initPlayer() {
      this.player = new YT.Player(this.$refs.videoPlayer.children[0], {
        events: {
          onReady: this.onPlayerReady,
        },
      });
    },
    onPlayerReady() {
      this.player.setVolume(this.volume);
    },
    playVideo() {
      this.player.playVideo();
      this.isPlaying = true;
    },
    pauseVideo() {
      this.player.pauseVideo();
      this.isPlaying = false;
    },
    stopVideo() {
      this.player.stopVideo();
      this.isPlaying = false;
    },
    toggleMute() {
      this.isMuted = !this.isMuted;
      this.isMuted ? this.player.mute() : this.player.unMute();
    },
    setVolume(event) {
      const volume = event.target.value;
      this.player.setVolume(volume);
    },
  },
};
</script>

<style scoped>
.youtube-player {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.video-container {
  width: 560px;
  height: 315px;
  position: relative;
  pointer-events: none; /* Disable pointer events to prevent interaction */
}

.video-frame {
  width: 100%;
  height: 100%;
  pointer-events: none; /* Disable pointer events on iframe */
}

.controls {
  margin-top: 10px;
}

.controls button {
  margin: 0 5px;
}

.controls input[type="range"] {
  width: 100px;
  margin-left: 10px;
}
</style>
