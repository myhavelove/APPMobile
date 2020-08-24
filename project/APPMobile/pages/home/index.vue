<template>
  <view class="container">
    <view class="example-body">
 

      <iv-nav-bar color="white" :status-bar="true"  title="修畸之家"  right-icon="chatbubble"  left-icon="phone"  background-color="#2ea8ab">
        <view slot="left"></view>
        <view slot="right">	<uni-badge class="uni-badge-left-margin" :text="badgeSun" type="error" size="small" /></view>
      </iv-nav-bar>
    </view>
    <!-- 搜索11 -->
    <view class="search-bar">
      <view class="search-bar-form">
        <view class="search-bar-box">
          <icon class="icon-search-in-box" type="search" :size="16"></icon>
          <input
            confirm-type="search"
            class="search-bar-input"
            placeholder="请输入案例编号/患者姓名"
            placeholder-class="phcolor"
            v-model="inputVal"
            @confirm="searchTap"
          />
          <view class="icon-clear" v-if="inputVal!=''" style="width: 5%;" @click="clearInput">
            <icon type="clear" :size="15"></icon>
          </view>
        </view>
      </view>
      <button class="btn-primary" hover-class="btn-hover" @tap="searchTap">搜索</button>
    </view>
    <!-- 搜索 -->
    <!--banner-->
    <view class="xz-banner-box">
      <swiper
        :indicator-dots="true"
        :autoplay="true"
        :interval="5000"
        :duration="150"
        class="xz-banner-swiper"
        :circular="true"
        indicator-color="rgba(255, 255, 255, 0.8)"
        indicator-active-color="#fff"
      >
        <swiper-item v-for="(item, index) in banner" :key="index" class="xz-banner-item">
          <image
            :src="imgHost + item.ImagerUrl"
            class="xz-slide-image"
            mode="scaleToFill"
            @tap="newsUrl(item.NewsUrl)"
          />
        </swiper-item>
      </swiper>
    </view>

    <!--banner-->

    <!-- 菜单盒子 -->
    <view class="example-menu">
      <iv-grid :column="3" :show-border="false" :highlight="true">
        <iv-grid-item v-for="(item, index) in menuList" :index="index" :key="index">
          <view class="grid-item-box" @tap="menuChange(item.topage)">
            <image :src="item.url" class="image" mode="aspectFill" />
            <text class="text">{{ item.text }}</text>
            <view v-if="item.badge" class="grid-dot">
							<uni-badge :text="item.badge" type="error" />
						</view>
          </view>
        </iv-grid-item>
      </iv-grid>
    </view>
    <!-- 菜单盒子 -->
    <!-- 在线客服 -->
    <iv-modal :show="contactModal" @cancel="hideModal" :custom="true">
      <view class="tui-modal-custom">
        <view class="xz-custom-text">客服电话：{{ contactPhone }}</view>
        <iv-button type="green" shape="circle" @click="dialClick(contactPhone)">拨号</iv-button>
      </view>
    </iv-modal>
    <!-- 在线客服 -->
  </view>
</template>
<script>
import ivIcons from "@/components/uni-icons/uni-icons.vue";
import ivGrid from "@/components/grid/uni-grid";
import ivGridItem from "@/components/grid-item/uni-grid-item";
import ivNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue";
import ivModal from "@/components/modal/modal";
import ivButton from "@/components/button/button";
export default {
  components: {
    ivIcons,
    ivGrid,
    ivGridItem,
    ivNavBar,
    ivModal,
    ivButton,
  },
  data() {
    return {
      contactModal: false, //modal弹框
      contactPhone: "4009696199",
      inputVal: "",
      imgHost: "",
      menuList: [{
          url:"../../static/menu/case-icon.png",
          text:"案例管理",
          topage:"",
          badge:3
      },{
          url:"../../static/menu/clinic-icon.png",
          text:"诊所管理",
          topage:"",
          badge:3
      },{
          url:"../../static/menu/doctor-icon.png",
          text:"医师管理",
          topage:"",
          badge:3
      }],
      badgeSun:'22',//右上角角标
      banner: [
        {
          ImagerUrl: "../../static/banner/1.png",
          NewsUrl: "",
        },
        {
          ImagerUrl: "../../static/banner/1.png",
          NewsUrl: "",
        },
      ],
    };
  },


  methods: {
    // 关闭modal
    hideModal() {
      this.contactModal = false;
    },
    // 打开modal
    serverBtn() {
      this.contactModal = true;
    },
    // 搜索
    searchTap() {},
    // 拨打电话
    dialClick(phone) {
      uni.makePhoneCall({
        // 手机号
        phoneNumber: phone,
        // 成功回调
        success: (res) => {
          console.log("调用成功!");
        },
        // 失败回调
        fail: (res) => {
          console.log("调用失败!");
        },
      });
    },
  },
};
</script>


<style scoped>
page {
  background: #f3f3f3 !important;
}

/*banner*/

.fl {
  float: left;
}

.uni-navbar__header {
  height: 68px;
}

.xz-banner-box {
  width: 100%;
  padding-top: 20rpx;
  box-sizing: border-box;
  background: #fff;
  padding-bottom: 20rpx;
  margin-bottom: 20rpx;
}

.xz-banner-swiper {
  width: 100%;
  height: 290rpx;
}

.xz-banner-item {
  padding: 0 16rpx;
  box-sizing: border-box;
}

.xz-slide-image {
  width: 100%;
  height: 290rpx;
  display: block;
  border-radius: 12rpx;
  /* transition: all 0.1s linear; */
}

.xz-banner-scale {
  transform: scaleY(0.9);
  transform-origin: center center;
}

/* #ifdef APP-PLUS || MP */
.xz-banner-swiper .wx-swiper-dot {
  width: 8rpx;
  height: 8rpx;
  display: inline-flex;
  background: none;
  justify-content: space-between;
}

.xz-banner-swiper .wx-swiper-dot::before {
  content: "";
  flex-grow: 1;
  background: rgba(255, 255, 255, 0.8);
  border-radius: 16rpx;
  overflow: hidden;
}

.xz-banner-swiper .wx-swiper-dot-active::before {
  background: #fff;
}

.xz-banner-swiper .wx-swiper-dot.wx-swiper-dot-active {
  width: 16rpx;
}

/* #endif */

/* #ifdef H5 */
.xz-banner-swiper .uni-swiper-dot {
  width: 8rpx;
  height: 8rpx;
  display: inline-flex;
  background: none;
  justify-content: space-between;
}

.xz-banner-swiper .uni-swiper-dot::before {
  content: "";
  flex-grow: 1;
  background: rgba(255, 255, 255, 0.8);
  border-radius: 16rpx;
  overflow: hidden;
}

.xz-banner-swiper .uni-swiper-dot-active::before {
  background: #fff;
}

.xz-banner-swiper .uni-swiper-dot.uni-swiper-dot-active {
  width: 16rpx;
}

/* #endif */
/* 自定义导航顶部消息 */
.uni-badge-left-margin{
    top: 37px;
    right: 0px;
    font-size: 12px;
    position: absolute;
    color: rgb(255, 255, 255);
    transform: translateY(0px) translateX(0px) scale(0.8);
}

/*banner*/


/* 九宫格 */
.example-menu {
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  padding: 0;
  font-size: 14px;
  background-color: #ffffff;
}

.grid-item-box {
  flex: 1;
  /* position: relative;
 */
  /* #ifndef APP-NVUE */
  display: flex;
  /* #endif */
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 15px 0;
}

.image {
  width: 95rpx;
  height: 95rpx;
}

.text {
  font-size: 26rpx;
  margin-top: 10rpx;
}
/* 九宫格角标 */
	.grid-dot {
		position: absolute;
		top: 5px;
		right: 15px;
	}
/* tb */
.bottom-container {
  height: 480rpx;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 60rpx 74rpx 40rpx 95rpx;
  background-color: #ffffff;
  border-radius: 10rpx;
  box-sizing: border-box;
  /* box-shadow: 0 0 10rpx #efefef; */
}

.ul-item {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.item {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
  width: 130rpx;
  height: 180rpx;
}

.item-img {
  width: 100rpx;
  height: 95rpx;
}

.item-name {
  padding-top: 13rpx;
  font-size: 24rpx;
  color: #666666;
  min-width: 80rpx;
  text-align: center;
}

.btn-feedback {
  background: transparent !important;
  position: absolute;
  height: 100%;
  width: 100%;
  left: 0;
  top: 0;
}

/* modal客服手机号 */
.xz-custom-text {
  text-align: center;
  padding: 10px;
}

/* 搜索功能 */

.search-bar {
  display: flex;
  align-items: center;
  position: relative;
  padding: 20upx 30upx 0upx;
  background-color: #fff;
  /* box-shadow: 0 2px 2px #ccc;*/
}

.search-bar-form {
  flex: 1;
  position: relative;
  border-radius: 32upx;
  background: #f2f5f7;
}

.search-bar-box {
  display: flex;
  align-items: center;
  position: relative;
  padding-left: 20upx;
  padding-right: 20upx;
  height: 64upx;
  z-index: 1;
}

.search-bar-input {
  line-height: normal;
  width: 100%;
  padding-left: 20upx;
  font-size: 30upx;
  color: #333;
}

.btn-primary {
  height: 62upx;
  width: 122upx;
  font-size: 30upx;
  line-height: 62upx;
  margin-left: 30upx;
  background: linear-gradient(-90deg, #1fc4d7, #1fc4d7);
  border-radius: 22px;
  color: #fff;
}

/* 数字消息 */
.orthodonticsNum,
.stateNum {
  padding: 3px 3px;
  overflow: hidden;
  float: left;
}
</style>