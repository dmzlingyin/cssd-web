
<template>
  <div class="demo-image__preview">
  <video id="video" controls></video>
  <video id="video" controls></video>
  <video id="video" controls></video>
  <video id="video" controls></video>
  </div>
</template>

<script>
// import axios from "axios";
import Hls from "@/dist/hls"

export default {
  data() {
    return {

    };
  },
  methods: {
  },
  mounted() {
    var video = document.getElementById('video');
    var videoSrc = "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8";
    if (Hls.isSupported()) {
      var hls = new Hls();
      hls.loadSource(videoSrc);
      hls.attachMedia(video);
    } else if (video.canPlayType("application/vnd.apple.mpegurl")) {
      video.src = videoSrc;
    }
  },
};
</script>

<style lang="scss">
#video {
  float: left;
  margin-left: 20px;
  margin-top: 30px;
  width: 500px;
  height: 300px;
}
</style>

