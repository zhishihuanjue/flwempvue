<template>
  <div class="image-item">
    <div class="">
        <image class="image"  :src="cardimage" role="img"> </image>
        <div class="title">{{text}}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['text','cardimage']
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


.view {
  display: block;
}


</style>
