<template>
 
    <div class="image-item" @click="skipDetails" >
      <div class="">
          <image class="image"  :src="cardimage" role="img"> </image>
          <div class="title">{{text}}</div>
      </div>
    </div>
   <!-- <a href="/pages/details/main">
  </a> -->
</template>

<script>
export default {
  props: ['text','cardimage'],
  data() {
    return {
      indicatorDots: true,
    }
  },
  methods: {
    skipDetails() {
      var url = "/pages/details/main";
       console.log('url'+url);
      wx.navigateTo({url})
    }
  }
}

</script>

<style>
.image-item {
  border: 2px solid #ffffff;
  border-radius: 5px;
  background-color: #ffffff;
  box-shadow: 0px 5px 1px #cccccc;
  margin: 8px;
  position: relative;
}

.image {
  width: 100%;
  height: 240px;
}

.title {
  font-size: 14px;
}
</style>
