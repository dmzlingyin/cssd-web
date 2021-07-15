
<template>
  <div class="demo-image__preview">
<!--    <div v-for="item in video" >-->
    <div v-for="item in 20" >
      <video width="320" height="260" controls autoplay>

        <source src='@/assets/a_mQtFtpPBB0iR1593536439.mp4' type="video/mp4">
<!--        <source :src=item.suource  type="video/mp4">-->
      </video>

    </div>


  </div>
</template>
<script>
import axios from "axios";

export default {
  data() {
    return {
      url: '@/assets/a_mQtFtpPBB0iR1593536439.mp4',
      video: [],
    }
  },
  methods: {
    click() {
      axios({
        url: 'http://127.0.0.1:5000/getNews',
        method: 'get',
        data: {
        }
      }).then(res => {
        console.log(res)
        this.video = res.data.video
      }).catch(err => {
        console.log(err)
      })
    }

  }
}
</script>

<style lang="scss">
.demo-image__preview{
  margin: 5px;
  display: flex;
  flex-wrap: wrap;
  div {
    margin-right: 10px;
  }
}
</style>

