<template>
	<view>
		<cu-custom  bgImage="http://q34h5h1tk.bkt.clouddn.com/header.jpeg"></cu-custom>
		<view class="page_bg"></view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				headImg: 'qqq'
			}
		},
		onLoad() {
		},
		methods: {

		}
	}
</script>
<style lang="scss">
	page{background-color:$uni-bg-color}
	.page_bg{
		width: 90%; 
		height: calc(100vh - 55px);
		margin: 0 auto;
		background-image: url('http://q34h5h1tk.bkt.clouddn.com/girl_bg.jpeg');
		background-size: 100% 100%;
	}
</style>
