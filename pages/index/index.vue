<template>
	<view>
		<cu-custom bgImage="https://facemark.skyvow.cn/uploads/fate_header_bg.jpg"></cu-custom>
		<view class="page_bg"></view>
		<button class="cu-btn btn web-font" @click="test()">开始预测</button>
		<!-- 遮罩层 -->
		<div class="cover" :class="className" @click='hide()'></div>
		<!-- 弹框 -->
		<view class="popup" id="capture" :class="className">
			<view class="border-r30 main border3">
				<view class="content">
					<image :src="shareImage" class="share-image" mode="aspectFit"></image>
					<canvasdrawer :painting="painting" class="canvasdrawer" @getImage="eventGetImage" />
				</view>
			</view>
			<view class="btn_box">
				<button class="cu-btn btn-retest" @click="save()" v-if='isAuth'>保存图片</button>
				<button class="cu-btn btn-retest" open-type="openSetting" v-if='!isAuth'>授权保存</button>
				<button class="cu-btn btn-share" open-type='share'>分享好友</button>
			</view>
		</view>
	</view>
</template>

<script>
	// import wakaryPoster from '@/components/wakary-poster/wakary-poster.vue'
	import canvasdrawer from "@/components/uniapp-canvas-drawer/uniapp-canvas-drawer"
	import utils from '@/common/utils.js';
	export default {
		components: {
			canvasdrawer
		},
		data() {
			return {
				isShow: false,
				painting: {},
				shareImage: '',
				isAuth: true,
				className: 'hide'
			}
		},
		onLoad() {},
		onShow() {
			let that = this;
			if (!that.isAuth) {
				//如果当前没有权限的话 就请求一下 是不是真的没有
				//还是在setting里设置里 但是状态没更新
				uni.authorize({
					scope: 'scope.writePhotosAlbum',
					success() {
						that.isAuth = true;
					},
					fail() {
						that.isAuth = false;
					}
				})
			}
		},
		methods: {
			getText() {
				let that = this;
				let textList = [];
				uni.request({
					url: utils.apiName + 'api/fate?is_show=1', //仅为示例，并非真实接口地址。
					success: function(res) {
						textList = res.data.data;
						//随机下标
						let index = parseInt(Math.random() * textList.length);
						let text = textList[index];
						that.painting = {
							width: 470,
							height: 720,
							clear: true,
							views: [{
									type: 'image',
									url: 'https://facemark.skyvow.cn/uploads/fate_body_bg.jpg',
									top: 0,
									left: 0,
									width: 470,
									height: 720
								},
								{
									type: 'image',
									url: utils.apiName + text.img,
									top: 14,
									left: 11,
									width: 450,
									height: 404,
									borderRadius: 20
								},
								{
									type: 'image',
									// url: 'https://facemark.skyvow.cn/uploads/fate_top_title.jpg',
									// http://q34h5h1tk.bkt.clouddn.com/2020%E8%BF%90%E5%8A%BF.png
									url: '../../static/img/title.png',
									top: 0,
									left: 135,
									width: 200,
									height: 47
								},
								{
									type: 'text',
									content: text.title,
									fontSize: 40,
									color: '#FFF',
									textAlign: 'left',
									top: 430,
									left: 44,
									width: 287,
									MaxLineNumber: 2,
									breakWord: true,
									bolder: true
								},
								{
									type: 'image',
									url: 'https://facemark.skyvow.cn/uploads/fate_qrcode.jpg',
									top: 434,
									left: 364,
									width: 76,
									height: 76
								},
								{
									type: 'text',
									content: text.desc,
									fontSize: 24,
									color: '#000',
									textAlign: 'left',
									top: 580,
									left: 34,
									lineHeight: 26,
									MaxLineNumber: 4,
									breakWord: true,
									width: 380
								}
							]
						}
					}
				});
			},
			test() {
				this.className = 'show';
				uni.showLoading({
					title: '分析中...',
					mask: true
				})
				setTimeout(() => {
					this.className = 'show fadeIn';
				}, 0);
				this.getText();
			},
			//关闭弹框
			hide() {
				this.className = 'show fadeOut';
				setTimeout(() => {
					this.className = 'hide';
				}, 300);
				this.shareImage = '../../static/img/empty.png';
			},
			save() {
				let that = this;
				uni.authorize({
					scope: 'scope.writePhotosAlbum',
					success() {
						that.isAuth = true;
						uni.saveImageToPhotosAlbum({
							filePath: that.shareImage,
							success(res) {
								uni.showToast({
									title: '保存图片成功',
									icon: 'success',
									duration: 2000
								})
							}
						})
					},
					fail() {
						that.isAuth = false;
					}
				})
			},
			eventGetImage(event) {
				uni.hideLoading();
				// const { tempFilePath, errMsg } = event.detail
				const result = event.detail.__args__
				const tempFilePath = result[0].tempFilePath
				const errMsg = result[0].errMsg
				if (errMsg === 'canvasdrawer:ok') {
					this.shareImage = tempFilePath
					this.painting = {}
				}
			}
		},
		onShareAppMessage(res) {
			if (res.from === 'button') { // 来自页面内分享按钮
				console.log(res.target)
			}
			return {
				title: '魔法测测：2020年...',
				path: '/pages/index/index',
			}
		}
	}
</script>
<style lang="scss">
	page {
		background-color: $uni-bg-color
	}

	.page_bg {
		width: 90%;
		height: calc(100vh - 85px);
		margin: 0 auto;
		background-image: url('https://facemark.skyvow.cn/uploads/fate_home_bg.jpg');
		background-size: 100% 100%;
		position: relative;
	}

	.btn {
		position: absolute;
		width: 260rpx;
		height: 80rpx;
		bottom: 100rpx;
		left: 0;
		right: 0;
		margin: 0 auto;
		border-radius: 40rpx;
		border: 6rpx solid #000;
		background-color: #FFB200 !important;
		text-align: center;
		font-size: 20px;
		font-weight: 1000;
		line-height: 68rpx;
	}

	.popup {
		position: absolute;
		left: 0;
		right: 0;
		top: 0;
		bottom: 0;
		margin: auto;
		z-index: 9999;
		width: 630rpx;
		height: 980rpx;
	}

	.popup .main {
		height: 880rpx;
		box-sizing: content-box;
		background-color: #F84033;
		display: flex;
		flex-direction: column;
		padding: 10rpx 30rpx;
		// background-image: url('http://q34h5h1tk.bkt.clouddn.com/result_bg.jpg');
		background-size: 100% 100%;
		justify-content: space-between;
	}

	.popup .main .box-top {
		height: 74%;
		background-color: #fd002e;
	}

	.popup .main .box-bottom {
		height: 24%;
		display: flex;
		align-items: center;
		padding: 0 30rpx;
	}

	.border3 {
		border: 3px solid #000;
	}

	.border-r30 {
		border-radius: 30rpx;
	}

	.center {
		margin: 0 auto;
		text-align: center;
	}

	// .title {
	// 	width: 200rpx;
	// 	position: absolute;
	// 	left: 0;
	// 	right: 0;
	// 	margin: 0 auto;
	// 	text-align: center;
	// 	height: 40rpx;
	// 	background-color: #F84033;
	// 	top: 10rpx;
	// }

	.box {
		width: 100%;
		border-radius: 30rpx;
		padding: 30rpx;
	}

	.show {
		display: block;
	}

	.hide {
		opacity: 0;
		display: none;
	}

	.cover {
		position: fixed;
		background: rgba(0, 0, 0, 0.8);
		width: 100%;
		height: 100%;
		z-index: 999;
		left: 0;
		top: 0;
	}



	.box-top image {
		overflow: hidden;
		border-top-left-radius: 24rpx;
		border-top-right-radius: 24rpx;
		width: 100%;
		height: 70%;
	}

	.title_box {
		height: 29%;
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 0 30rpx;
		color: #FFF;
		font-size: 48rpx;
		font-weight: 900;
	}

	.title_box .qcode {
		width: 130rpx;
		height: 130rpx;
		background: #FFF;
	}

	.btn_box {
		width: 100%;
		margin-top: 20rpx;
		display: flex;
		justify-content: space-around;
	}

	.btn_box button {
		width: 45%;
		height: 80rpx;
		font-size: 40rpx;
		border-radius: 40rpx;
		color: #FFF;
	}

	.btn-retest {
		background-image: radial-gradient(#283fdf, #009af5);
	}

	.btn-share {
		background-image: radial-gradient(#fd002e, #fd6f1f);
	}

	.share-image {
		width: 600upx;
		height: 888upx;
	}

	@keyframes fadeIn {
		0% {
			opacity: 0;
		}

		to {
			opacity: 1;
		}
	}

	.fadeIn {
		animation: fadeIn ease .3s forwards;
		
	}

	@keyframes fadeOut {
		0% {
			opacity: 1;
		}

		to {
			opacity: 0;
		}
	}

	.fadeOut {
		animation: fadeOut ease .3s forwards;
	}
</style>
