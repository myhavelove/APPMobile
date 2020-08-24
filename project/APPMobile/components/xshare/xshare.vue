<template>
	<view>
		<uni-popup ref="sharebox" :mask-click="true" type="bottom">
			<view class="poster">
				<view class="content02">
					<view class="">
						<image class="image" :src="posterImg" mode="aspectFit" />
					</view>
				</view>
				<text class="test" @click="cancelPopup">&#xe60d;</text>
			</view>
			<view class="uni-share">
				<view class="uni-share-content">
					<view class="uni-share-content-box">
						<button open-type="share" @click="clickShare('wx')" plain="true" class="add">
							<view class="uni-share-content-image">
								<image src="/static/sharemenu/wx.png" class="content-image" mode="widthFix" />
							</view>
							<text class="uni-share-content-text">分享好友</text>
						</button>
					</view>
					<view class="uni-share-content-box" @click="clickShare('pic')">
						<button plain="true" class="add">
							<view class="uni-share-content-image">
								<image src="/static/sharemenu/pyq.png" class="content-image" mode="widthFix" />
							</view>
							<text class="uni-share-content-text">保存海报</text>
						</button>
					</view>
				</view>
			</view>
			
		</uni-popup>
	</view>
</template>

<script>
	import uniPopup from '@/components/uni-popup/uni-popup.vue'
	import {
		http
	} from '@/utils/luch-request/index.js'
	import util from '@/utils/util.js'

	export default {
		components: {
			uniPopup
		},
		props: {
			sharecode: {
				type: String,
				default: ''
			},
			sharetype: {
				type: String,
				default: ''
			}
		},
		data() {
			return {
				posterImg: '',
				shareTitle: '',
				shareUrl: ''
			};
		},
		onShareAppMessage(res) {
			return {
				title: this.shareTitle,
				path: this.shareUrl
			}
		},
		methods: {
			togglePopup() {
				this.shareopen(this.sharetype, this.sharecode);
				this.$nextTick(() => {
					this.$refs['sharebox'].open();
				})
			},
			cancelPopup() {
				this.$refs['sharebox'].close();
			},
			clickShare(index) {
				if (index == "wx") {

				} else if (index == "pic") {
					util.downLoadImage(this, this.posterImg);
				}
				this.cancelPopup();
			},
			shareopen() {
				console.log(this.sharetype)
				var that = this;
				http.post('Vip/QueryShare', {
					"type": this.sharetype,
					"code": this.sharecode
				}).then(res => {
					if (res != undefined) {
						console.log(res)
						that.posterImg = res.data.data.ShareImgUrl;
						that.shareTitle = res.data.data.Title;
						that.shareUrl = "/" + res.data.data.ShareUrl + "?" + res.data.data.Sence;
					}
				})
			}
		}
	}
</script>

<style>
	.test{font-family: "iconfont" !important;font-size: 60rpx; color: #FFFFFF; position: absolute; bottom: 200rpx; right: 330rpx;}
	#share {
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
		border-top-left-radius: 20rpx;
		border-top-right-radius: 20rpx;
	}

	.add{
		line-height: 40rpx !important;
		border: 1px solid #FFFFFF !important;
	}
	.add::after{ border: none; }

	/* 底部分享 */
	.uni-share {
		/* #ifndef APP-NVUE */
		display: flex;
		flex-direction: column;
		/* #endif */
		background-color: #fff;
	}

	.uni-share-title {
		line-height: 60rpx;
		font-size: 24rpx;
		padding: 15rpx 0;
		text-align: center;
	}

	.uni-share-content {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: center;
		padding: 15px;
	}

	.uni-share-content-box {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		align-items: center;
		width: 200rpx;
	}

	.uni-share-content-image {
		/* #ifndef APP-NVUE */
		/* display: flex; */
		/* #endif */
		/* flex-direction: row;
		justify-content: center;
		align-items: center;
		width: 60rpx;
		height: 60rpx;
		overflow: hidden;
		border-radius: 10rpx; */
	}

	.content-image {
		width: 80rpx;
		height: 80rpx;
	}

	.uni-share-content-text {
		font-size: 26rpx;
		color: #333;
		padding-top: 5px;
		padding-bottom: 10px;
	}

	.uni-share-btn {
		height: 90rpx;
		line-height: 90rpx;
		font-size: 14px;
		border-top-color: #f5f5f5;
		border-top-width: 1px;
		border-top-style: solid;
		text-align: center;
		color: #666;
	}

	/* 专属海报 */
	/* .big-box {
		width: 100%;
		height: 100%;
		background: rgb(0, 0, 0, 0.6);
		filter: progid:DXImageTransform.Microsoft.gradient(startColorstr=#99000000, endColorstr=#99000000);
		position: fixed;
		left: 0;
		right: 0;
		top: 0;
		z-index: 99999;
	} */

	.buttom {
		width: 100%;
		height: 90rpx;
		line-height: 90rpx;
		border-top: 1px solid #f3f3f3;
		font-size: 32rpx;
		display: flex;
		text-align: center;
		position: absolute;
		bottom: 0;
		left: 0;
		right: 0;
	}

	.buttom view {
		width: 50%;
		color: #999;
	}

	/* .content {
		width: 100%;
		height: 540rpx;
		position: relative;
	} */

	.copy {
		color: #f39800 !important;
		border-left: 1px solid #f3f3f3;
	}

	/* 	.poster {
		width: 86%;
		height: 1000rpx;
		background: #fff;
		border-radius: 10px;
		position: absolute;
		left: 50%;
		margin-left: -43%;
		top: 50%;
		margin-top: -500rpx;
	} */

	.image {
		width: 535rpx;
		height: 855rpx;
		display: block;
		margin: 0 auto;
		border-radius: 20rpx;
	}

	.content02 {
		width: 100%;
		position: relative;
		top: -80rpx;
		/* height: 1000rpx; */
	}

	/* 专属海报end */
</style>
