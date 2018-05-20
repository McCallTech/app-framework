<!-- Initial page of the main view, please see ../app.vue for more information about the application layout -->

<template>
  <f7-page>

    <!-- Navbar -->
    <f7-navbar sliding :title="$root.config.title">
      <f7-nav-right v-if="$root.user"><f7-link icon-material="person" open-popup="#app-framework-login-popup" /></f7-nav-right>
    </f7-navbar>

    <!-- Installation notice -->
    <f7-block inner inset style="text-align: center" v-if="$root.appMode==='mobile'">
      <p><b>For native App feeling, please pin this page to your homescreen and open it from there!</b></p>
    </f7-block>
   <video-player class="video-player-box"
                 ref="videoPlayer"
                 :options="playerOptions"
                 :playsinline="true"
                 customEventName="customstatechangedeventname"

                 @play="onPlayerPlay($event)"
                 @pause="onPlayerPause($event)"
                 @ended="onPlayerEnded($event)"
                 @statechanged="playerStateChanged($event)"
                 @ready="playerReadied">
  </video-player>
  </f7-page>
</template>

<script>
import 'video.js/dist/video-js.min.css';
import { videoPlayer } from 'vue-video-player';
import 'videojs-youtube/dist/Youtube.min';
module.exports = {
  data: function() {
    return {
      playerOptions: {
        // videojs options
        muted: true,
        language: 'en',
        playbackRates: [0.7, 1.0, 1.5, 2.0],
        techOrder: ['youtube'],
        sources: [
          {
            type: 'video/youtube',
            src: 'https://www.youtube.com/embed/0L-6ls2Rrgc'
          }
        ]
      },
      images: {
        flag_en: require('../images/flag-en.png'),
        flag_de: require('../images/flag-de.png'),
        theme_ios: require('../images/theme-ios.png'),
        theme_material: require('../images/theme-material.png'),
        firebase: require('../images/firebase.png')
      }
    };
  },
  components: {
    videoPlayer
  },
  mounted() {
    console.log('this is current player instance object', this.player);
  },
  computed: {
    player() {
      return this.$refs.videoPlayer.player;
    }
  },
  methods: {
    updateSmartlist: function(e) {
      setTimeout(
        function() {
          let text = this.$$(e.target)
            .find('option[value=' + e.target.value + ']')
            .text();
          this.$$(e.target)
            .parent()
            .find('.item-after')
            .html(text);
        }.bind(this),
        0
      );
    },
    // listen event
    onPlayerPlay(player) {
      // console.log('player play!', player)
    },
    onPlayerPause(player) {
      // console.log('player pause!', player)
    },
    // or listen state event
    playerStateChanged(playerCurrentState) {
      // console.log('player current update state', playerCurrentState)
    },
    // player is ready
    playerReadied(player) {
      console.log('the player is readied', player);
    }
  }
};
</script>

<style>
.f7-icons {
  width: 29px;
  font-size: 29px;
  height: 29px;
  text-align: center;
  color: gray;
}
</style>
