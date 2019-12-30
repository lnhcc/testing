<template>
	<view>
		<cu-custom bgImage="http://q34h5h1tk.bkt.clouddn.com/header.jpeg"></cu-custom>
		<view class="page_bg"></view>
		<button class="cu-btn btn web-font" @click="test()">开始预测</button>
		<!-- 遮罩层 -->
		<div class="cover" :class="isShow?'show':'hide'" @click='hide()'></div>
		<!-- 弹框 -->
		<view class="popup" id="capture" :class="isShow?'show':'hide'">
			<view class="border-r30 main border3">
				<view class="border-r30 border3 box-top">
					<image :src="imgUrl"></image>
					<view class="title_box">
						<view class="title ">
							{{title}}<br>{{title2}}
						</view>
						<view class="qcode border3">
						</view>
					</view>
				</view>
				<view class="border-r30 border3 box-bottom">
					{{descripte}}
				</view>
			</view>
			<view class="btn_box">
				<button class="cu-btn btn-retest" @click="save()">保存图片</button>
				<button class="cu-btn btn-share" @click="share()" open-type='share'>立即分享</button>
			</view>
		</view>

		<!-- <wakary-poster>

		</wakary-poster> -->

	</view>
</template>

<script>
	// import wakaryPoster from '@/components/wakary-poster/wakary-poster.vue'
	export default {
		components: {
			// wakaryPoster
		},
		data() {
			return {
				isShow: true,
				title: '桃花旺，人品好',
				title2: '火速脱单',
				imgUrl: '../../static/img/img.jpeg',
				descripte: '没错，你就是靠脸吃饭的代表，乡亲父老的国宝，被星探发现，从此开启演艺之路。拍广告上春晚出人头地不是梦。2020星运超旺'
			}
		},
		onLoad() {

		},
		methods: {
			test() {
				this.isShow = !this.isShow;
				console.log(1111)
			},
			//关闭弹框
			hide() {
				this.isShow = !this.isShow;
			},
			//保存图片
			save() {
				console.log(111);
				
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
		background-image: url('http://q34h5h1tk.bkt.clouddn.com/girl_bg.jpg');
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
		height: 800rpx;
		box-sizing: content-box;
		background-color: #F84033;
		display: flex;
		flex-direction: column;
		padding: 30rpx;
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
</style>
