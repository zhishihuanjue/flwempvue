<template>
 
    <div class="image-item" @click="skipDetails" >
      <image class="image"  :src="cardimage" role="img"> </image>
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
  background-color: #ffffff;
  margin: 10px;
  position: relative;
}

.image {
  width: 100%;
  height: 240px;
  -moz-border-radius: 5px;
  -webkit-border-radius: 5px;
  border-radius: 5px;
}

</style>
