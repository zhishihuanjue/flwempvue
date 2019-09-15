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
            <icon class="weui-icon-search_in-box" type="search" color="rgb(184,95,97)" size="20"></icon>
            <div class="searchfont"><a href="/pages/test/main" >{{inputVal}}</a></div>
          </div>
        </navigator>
      </div>

      <!-- 选项卡 -->
      <div class="kind-list">
        <div class="kind-list__item">
            <div class="weui-navbar1">
              <block v-for="(item,index) in list" :key="index">
                <div :id=item.id  :data-index="index" :class="{'weui-bar__item_on':activeIndex == index}" class="weui-navbar__item" @click="tabClick">
                  <div class="weui-navbar__title">{{item.name}}</div>
                </div>
              </block>
            </div>
            <div v-for="(item,index) in list" :key="index" :class="{'kind-list__item-bd_show':item.open}" class="kind-list__item-bd">
              <div :class="{'weui-cells_show':item.open}" class="weui-cells weui-cells1" >
                  <div class="page__bd page__bd_spacing">
                    <div class="weui-flex1"   >
                      <div class="weui-flex__item1" v-for="(page,i) in item.pages" :key="i" >
                        <div :class="{'placeholder_show':page.ischek}" class="placeholder" >{{page.name}}</div>
                      </div>
                    </div>
                  </div>
              </div>
            </div>
        </div>
      </div>

      <!-- 图片item -->
      <div class="img-items">
          <card  v-for="(dataImg,index) in dataImgs"  :key="index" :text="dataImg.text" :cardimage="dataImg.img" ></card>
      </div>

    </div>
  </div>
</template>

<script>
import card from '@/components/card'

export default {
  onReachBottom(){
      var thar = this;
    // 上拉加载更多
      console.log("// 上拉加载更多");
      wx.showLoading({
        title: '加载中',
      });
      setTimeout(function () {
        wx.hideLoading();
        thar.dataImgs.push({"img":"http://manager.ddroom.cn//upload/render/20190909172050/09dcc43b.jpg","text":"设计师:yangji"});
      }, 2000)
  },
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
      fontSize: 30,
      list: [
        {
          id: 'kongjian',
          cid: "qbkj",
          name: '全部空间',
          open: false,
          pages: [{id:"qbkj",name:"全部空间",ischek:true},{id:"kt",name:"客厅",ischek:false},{id:"woshi",name:"卧室",ischek:false},
           {id:"etf",name:"儿童房",ischek:false}, {id:"cf",name:"厨房",ischek:false}]
        },
        {
          id: "leixing",
          cid: "qblx",
          name: "全部类型",
          open: false,
          pages: [{id:"qblx",name:"全部类型",ischek:true}, {id:"yimaojian",name:"衣帽间",ischek:false}, {id:"jiugui",name:"酒柜",ischek:false},
           {id:"yigui",name:"衣柜",ischek:false}, {id:"chuwuge",name:"储物柜",ischek:false}, {id:"shuzuo",name:"书桌",ischek:false},{id:"shuzuo",name:"茶几",ischek:false}]
        },
        {
          id: 'ertfang',
          cid: "qbfg",
          name: '全部风格',
          open: false,
          pages: [{id:"qbfg",name:"全部风格",ischek:true},{id:"beiou",name:"北欧",ischek:false},
          {id:"xiantai",name:"现代",ischek:false},{id:"qinshe",name:"轻奢",ischek:false},{id:"zhongshi",name:"中式",ischek:false},{id:"dizhonghai",name:"地中海",ischek:false}]
        },
        {
          id: 'huxing',
          cid: "qbhx",
          name: '全部户型',
          open: false,
          pages: [{id:"qbhx",name:"全部户型",ischek:true},{id:"yishi",name:"一室",ischek:false}, {id:"liangshi",name:"两室",ischek:false}, {id:"sanshi",name:"三室",ischek:false}]
        }
      ]
    }
  },
  components: {
    card
  },
  computed: {
    
  },
  created(){
   
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
      var id = e.currentTarget.id;
      this.activeIndex = e.currentTarget.dataset.index;
      var list = this.list;
      for (var i = 0, len = list.length; i < len; ++i) {
        if (list[i].id === id) {
          list[i].open = !list[i].open;
        } else {
          list[i].open = false;
        }
      }
      this.list = list;
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

.weui-search-bar__cancel-btn{
  color: #000000;
  font-size: 30rpx;
}

.searchfont{
  font-size: 30rpx;
}


/*图片样式*/

.img-items{
  background-color:#ffffff;
  padding: 0px; 
} 

.weui-navbar{
  background-color:#ffffff;
}

.weui-flex__item1{
    width:25%;
}

.weui-flex1 {
  flex-wrap: wrap;
  width: 100%;
  display: flex;
  -webkit-box-align: center;
  -webkit-align-items: center;
  align-items: center;
}
  

  .placeholder {
    font-size: 30rpx;
    margin: 5px;
    padding: 0 10px;
    text-align: center;
    background-color: #f8f8f8;
    height: 2.3em;
    line-height: 2.3em;
    color: #afafaf;
  }

  .weui-navbar__item.weui-bar__item_on {
      color: #b85f61;
  }


  .placeholder_show {
    color:#b85f61;
    background-color: #f9f2df;
    /* background-color:#cbbca6; */
    /* background-color: #1aad19; */
  }


 .weui-navbar1 {
    display: -webkit-box;
    display: -webkit-flex;
    display: flex;
    z-index: 500;
    top: 0;
    width: 100%;
    border-bottom: 1rpx solid #f8f8f8;
}

.weui-cells1 {
  margin-top: 0;
  opacity: 0;
  -webkit-transform: translateY(-50%);
  transform: translateY(-50%);
  -webkit-transition: 0.3s;
  transition: 0.3s;
}

.weui-cells1:after,
.weui-cells1:before {
  display: none;
}

.weui-cells_show {
  opacity: 1;
  -webkit-transform: translateY(0);
  transform: translateY(0);
}

.weui-cell:before {
  right: 15px;
}

.kind-list__item {
  margin: 10px 0;
  background-color: #fff;
  border-radius: 2px;
  overflow: hidden;
}

.kind-list__item:first-child {
  margin-top: 0;
}

.kind-list__img {
  width: 30px;
  height: 30px;
}

.kind-list__item-hd {
  padding: 20px;
  -webkit-transition: opacity 0.3s;
  transition: opacity 0.3s;
}

.kind-list__item-hd_show {
  opacity: 0.4;
}

.kind-list__item-bd {
  width: 100%;
  z-index: 99999;
  position:absolute;
  height: 0;
  overflow: hidden;
}

.kind-list__item-bd_show {
  height: auto;
}

</style>

