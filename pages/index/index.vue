<template>
	<view>
		<cu-custom bgImage="http://q34h5h1tk.bkt.clouddn.com/header.jpeg"></cu-custom>
		<view class="page_bg"></view>
		<button class="cu-btn btn web-font" @click="test()">开始预测</button>
		<!-- 遮罩层 -->
		<div class="cover" :class="isShow?'show':'hide'"></div>
		<!-- 弹框 -->
		<view class="popup border2" :class="isShow?'show':'hide'">

		</view>

		<!-- <wakary-poster>

		</wakary-poster> -->

	</view>
</template>

<script>
	import wakaryPoster from '@/components/wakary-poster/wakary-poster.vue'
	export default {
		components: {
			wakaryPoster
		},
		data() {
			return {
				isShow: false
			}
		},
		onLoad() {},
		methods: {
			test() {
				this.isShow = !this.isShow;
				console.log(1111)
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
		width: 600rpx;
		height: 800rpx;
		background-color: #F84033;
		display: flex;
		position: absolute;
		left: 0;
		right: 0;
		margin: auto;
		top: 0rpx;
		bottom: 0;
		border-radius: 30rpx;
		padding: 30rpx;
		background-image: url('http://q34h5h1tk.bkt.clouddn.com/result_bg.jpg');
		background-size: 100% 100%;
			z-index: 9999;
	}

	.border2 {
		border: 2px solid #000;
	}

	.border4 {
		border: 4px solid #000;
	}

	.center {
		margin: 0 auto;
		text-align: center;
	}

	.title {
		width: 200rpx;
		position: absolute;
		left: 0;
		right: 0;
		margin: 0 auto;
		text-align: center;
		height: 40rpx;
		background-color: #F84033;
		top: 10rpx;
	}

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
		
		background:rgba(0, 0, 0, 0.8);
		width: 100%;
		height: 100%;
		z-index: 999;
		left: 0;
		top: 0;
	}
</style>
