<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <video id="myvideo" ref="myVideo" src="http://babylife.qiniudn.com/FtRVyPQHHocjVYjeJSrcwDkApTLQ" poster="http://static.fdc.com.cn/avatar/usercenter/5996999fa093c04d4b4dbaf1_162.jpg" height="414" width="720">
      your browser does not support the video tag
    </video>
    <!-- <span class="ico ico-sound" :class="{ active: isMute }" v-on:click="closeSoundClick()"></span> -->
    <!-- <span class="ico ico-skip"></span> -->
    <span class="ico ico-video" :class="{ hide: isPlay }" v-on:click="playClick()">{{text}}</span>

    <video-player class="video-player vjs-custom-skin" ref="videoPlayer" :playsinline="true" :options="playerOptions" @play="onPlayerPlay($event)" @pause="onPlayerPause($event)">
    </video-player>
  </div>
</template>

<script>
require('video.js/dist/video-js.css');
require('vue-video-player/src/custom-theme.css');

import Vue from 'vue';
import VideoPlayer from 'vue-video-player';
Vue.use(VideoPlayer);
export default {
  name: 'HelloWorld',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      _dom: '',
      isPlay: false,
      text: '开始播放',
      // video-player
      playerOptions: {
        //        playbackRates: [0.7, 1.0, 1.5, 2.0], //播放速度
        autoplay: false, //如果true,浏览器准备好时开始回放。
        muted: false, // 默认情况下将会消除任何音频。
        loop: false, // 导致视频一结束就重新开始。
        preload: 'auto', // 建议浏览器在<video>加载元素后是否应该开始下载视频数据。auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
        language: 'zh-CN',
        aspectRatio: '16:9', // 将播放器置于流畅模式，并在计算播放器的动态大小时使用该值。值应该代表一个比例 - 用冒号分隔的两个数字（例如"16:9"或"4:3"）
        fluid: true, // 当true时，Video.js player将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
        sources: [
          {
            type: 'video/mp4',
            src: 'http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4' //你的视频地址（必填）
          }
        ],
        poster:
          'http://static.fdc.com.cn/avatar/usercenter/5996999fa093c04d4b4dbaf1_162.jpg', //你的封面地址
        width: document.documentElement.clientWidth,
        notSupportedMessage: '此视频暂无法播放，请稍后再试' //允许覆盖Video.js无法播放媒体源时显示的默认信息。
        //        controlBar: {
        //          timeDivider: true,
        //          durationDisplay: true,
        //          remainingTimeDisplay: false,
        //          fullscreenToggle: true  //全屏按钮
        //        }
      }
    };
  },
  computed: {
    player() {
      return this.$refs.videoPlayer.player;
    }
  },
  methods: {
    playClick() {
      // this._dom = document.getElementById('myvideo');
      // this._dom = document.getElementsByClassName('myvideo')[0];
      this._dom = this.$refs.myVideo;
      this.isPlay = !this.isPlay;
      if (this.isPlay) {
        this._dom.play();
        this.text = '暂停';
      } else {
        this._dom.pause();
        this.text = '开始播放';
      }
    },
    /**
     * desc:视频播放按钮操作
     */
    onPlayerPlay(player) {
      // alert('play');
    },
    onPlayerPause(player) {
      // alert('pause');
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
