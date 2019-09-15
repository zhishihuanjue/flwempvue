<template>
  <div class="page">
    <div class="page__bd page__bd_spacing">
      <swiper :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration" :circular="circular" @change="swiperChange" @animationfinish="animationfinish">
        <div v-for="(item,index) in imgUrls" :key="index" >
          <swiper-item>
            <image :src="item" class="slide-image" @click="previewImage(item)" />
          </swiper-item>
        </div>
      </swiper>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      indicatorDots: true,
      autoplay: true,
      interval: 5000,
      duration: 900,
      circular: true,
      imgUrls: [
        'http://manager.ddroom.cn//upload/render/20190905161748/367850f9.jpg',
        'http://manager.ddroom.cn//upload/render/20190909172050/09dcc43b.jpg',
        'http://manager.ddroom.cn//upload/render/20190908172902/da5bcd1b.jpg'
      ]
    }
  },
  methods: {
    previewImage(src){
      let that = this;
      wx.onWindowResize(function(res) {
          console.log("res" + res.deviceOrientation);
          if (res.deviceOrientation === 'landscape') {
              that.isRotating = true;
          } else {
              that.isRotating = false;
          }
      })
      wx.previewImage({
        current:src, // 当前显示图片的http链接
        urls: this.imgUrls // 需要预览的图片http链接列表
      })
    },
    swiperChange(e) {
      console.log('第' + e.mp.detail.current + '张轮播图发生了滑动');
    },
    animationfinish(e) {
      console.log('第' + e.mp.detail.current + '张轮播图滑动结束');
    }
  }
}
</script>

<style>
.slide-image {
  width: 100%;
  height: 100%;
}
</style>