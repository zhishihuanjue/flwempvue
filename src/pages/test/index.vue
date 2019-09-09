<template>
  <div class="page">
    <div class="page__bd">
      <!-- 搜索框 -->
      <div class="weui-search-bar">
        <div class="weui-search-bar__form">
          <div class="weui-search-bar__box">
            <icon class="weui-icon-search_in-box" type="search" size="14"></icon>
            <input type="text" class="weui-search-bar__input" placeholder="搜索" v-model="inputVal" :focus="inputShowed" @input="inputTyping" />
            <div class="weui-icon-clear" v-if="inputVal.length > 0" @click="clearInput">
              <icon type="clear" size="14"></icon>
            </div>
          </div>
          <label class="weui-search-bar__label" :hidden="inputShowed" @click="showInput">
            <icon class="weui-icon-search" type="search" size="14"></icon>
            <div class="weui-search-bar__text">搜索</div>
          </label>
        </div>
        <div class="weui-search-bar__cancel-btn" :hidden="!inputShowed" @click="hideInput">取消</div>
      </div>
      <div class="weui-cells searchbar-result" v-if="inputVal.length > 0">
        <navigator url="" class="weui-cell" hover-class="weui-cell_active">
          <div class="weui-cell__bd">
            <div>实时搜索文本</div>
          </div>
        </navigator>
      </div>

      <!-- 选项卡 -->
      <div class="weui-tab">
        <div class="weui-navbar">
          <block v-for="(item,index) in tabs" :key="index">
            <div :id="index" :class="{'weui-bar__item_on':activeIndex == index}" class="weui-navbar__item" @click="tabClick">
              <div class="weui-navbar__title">{{item}}</div>
            </div>
          </block>
          <div class="weui-navbar__slider" :class="navbarSliderClass"></div>
        </div>
        <div class="weui-tab__panel">
          <!-- 图片item -->
          <div class="img-items">
            <template v-for="(dataImg,index) in dataImgs">
              <card :text="dataImg.text" :cardimage="dataImg.img"  ></card>
            </template>
          </div>
        </div>
      </div>

     

    </div>
  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data() {
    return {
      user:{},
      dataImgs:[
      {"img":"http://manager.ddroom.cn//upload/render/20190905161748/367850f9.jpg","text":"设计师:云纺店张艳玲"},
      {"img":"http://manager.ddroom.cn//upload/render/20190905161748/367850f9.jpg","text":"设计师:云纺店张艳玲"},
      {"img":"http://manager.ddroom.cn//upload/render/20190905161748/367850f9.jpg","text":"设计师:云纺店张艳玲"}],
      inputShowed: false,
      inputVal: "",
      tabs: ["客厅", "卧室", "儿童房","卫生间","厨房"],
      activeIndex: 0,
      fontSize: 30
    }
  },
  components: {
    card
  },
  computed: {
    navbarSliderClass() {
      if (this.activeIndex == 0) {
        return 'weui-navbar__slider_0'
      }
      if (this.activeIndex == 1) {
        return 'weui-navbar__slider_1'
      }
      if (this.activeIndex == 2) {
        return 'weui-navbar__slider_2'
      }
      if (this.activeIndex == 3) {
        return 'weui-navbar__slider_3'
      }
      if (this.activeIndex == 4) {
        return 'weui-navbar__slider_4'
      }
    }
  },
  created(){
    wx.login({
      success (res) {
          if (res.code){
              console.log(res.code);
              // 这里可以把code传给后台，后台用此获取openid及session_key
          }
      },
    })
    wx.getUserInfo({
      success: function (res) {
        console.log(res.userInfo.nickName);
        console.log(res.userInfo.avatarUrl);
      },
    })
  },
  methods: {
    showInput() {
      this.inputShowed = true;
    },
    hideInput() {
      this.inputVal = '';
      this.inputShowed = false
    },
    clearInput() {
      this.inputVal = '';
    },
    inputTyping(e) {
      console.log(e);
      this.inputVal = e.mp.detail.value
    },
    tabClick(e) {
      console.log(e);
      this.activeIndex = e.currentTarget.id;
    }
  }
}
</script>

<style scoped>

page,
.page,
.page__bd {
  height: 100%;
}
.page__bd {
  padding-bottom: 0;
}

.searchbar-result {
  margin-top: 0;
  font-size: 14px;
}
.searchbar-result:before {
  display: none;
}
.weui-cell {
  padding: 12px 15px 12px 35px;
}
.weui-tab__content {
  padding-top: 60px;
  text-align: center;
}
.weui-navbar__slider_0 {
  left: 29rpx;
  transform: translateX(0);
}
.weui-navbar__slider_1 {
  left: 29rpx;
  transform: translateX(150rpx);
}
.weui-navbar__slider_2 {
  left:29rpx;
  transform: translateX(300rpx);
}
.weui-navbar__slider_3 {
  left:29rpx;
  transform: translateX(450rpx);
}
.weui-navbar__slider_4 {
  left:29rpx;
  transform: translateX(600rpx);
}

.weui-navbar__slider {
  position: absolute;
  content: " ";
  left: 0;
  bottom: 0;
  width: 4em;
  height: 3px;
  background-color: #1aad19;
  -webkit-transition: -webkit-transform 0.3s;
  transition: -webkit-transform 0.3s;
  transition: transform 0.3s;
  transition: transform 0.3s, -webkit-transform 0.3s;
}

/*图片样式*/

.img-items{
  background-color:#f4f4f4;
  padding: 0px; 
} 

.weui-navbar{
  background-color:#ffffff;
}

.weui-tab__panel{
  background-color:#f4f4f4;
}

</style>