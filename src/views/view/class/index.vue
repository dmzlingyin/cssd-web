 author:李瑞沂   data：2021-8-1

<template>
<div>
  <!-- v-for  循环自动生成盒子 -->
  <div class="demo-image__preview" v-for="item in URI" :key="item.uri">
    <video class="video"  v-bind:id="item.uri" controls ></video>
  </div>
  </div>
</template>

<script>
import Hls from "@/dist/hls";
export default {
  
  data() {
   
    return {
        URL :[
         {url: "http://localhost:8080"} ,
         {url: "http://localhost:8080"} ],
        
        URI :[
          {uri: "rtsp://192.168.50.34:8554/mystream"},
          {uri: "rtsp://192.168.50.34:8554/mystreak"}
          ],
      startStream: "",
       axios: require("axios"),
    };
  },
  methods: {},
  mounted() {
    var that = this;
    let videoSrc = "";
    var i = 0;
    var video;
    //startStream函数-----将uri解析为m3u8格式的url
    that.startStream = async function (uri) {
      //  for循环遍历uri,异步原因，for循环位置有要求
      for(i;i<1;i++){
         
         await this.axios.post(`${this.URL[i].url}/start`, { uri }).then(res=>{
           //将 v-for和for循环连接起来
         video = document.getElementById(this.URI[i].uri);
         //将解析出来的url给videoSrc 
         videoSrc = res.data.uri;
         //连接为一个完整的url
         videoSrc = `${this.URL[i].url}${videoSrc}`;
         //  Hls推流部分
         if (Hls.isSupported()) {
            var hls = new Hls();
            hls.loadSource(videoSrc);
            hls.attachMedia(video);
          } else if (video.canPlayType("application/vnd.apple.mpegurl")) {
            video.src = videoSrc;
          }
       });
    };
    }
    //调用多次startStream函数
    for(var j = 0;j <2;j++){
      that.startStream(this.URI[j].uri);
    }

  },
};
//-----------暂时未用到的函数listStreams
// for(i=0;i<2;i++){
    
//     // that.listStreams = function () {
//     //     return that.axios.get(`${that.url}/list`).then((res) => {
//     //       console.log(res.data);
//     //       return res.data.map(({ uri }) => `${that.url}${uri}`);
//     //     });
//     //   };
//      that.startStream(this.URI[i].uri).then((res) => {
//        videoSrc = res.data.uri;
//        videoSrc = `${this.URL[i].url}${videoSrc}`
//        console.log(videoSrc);
//       // that.listStreams().then((res) => {
//       //   console.log(res);
//         // for(var i = 0;i < res.length;i ++){
//           if (Hls.isSupported()) {
//           var hls = new Hls();
//           hls.loadSource(videoSrc);
//           hls.attachMedia(video);
//           } else if (video.canPlayType("application/vnd.apple.mpegurl")) {
//             video.src = videoSrc;
//           }
//         // }
//       // });
//     });

// }
</script>

<style lang="scss">
//外面盒子样式
.demo-image__preview{
 display: inline-block;
 margin-left: 20px;
  width: 500px;
  height: 300px;
}
.video {
  
  object-fit:fill;
  float: left;
  margin-left: 20px;
  margin-top: 30px;
  width: 100%;
  height: 100%;
 
}
</style>

