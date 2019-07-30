<template>
	<view class="myCreditbox">
		<view class="topCont center white">
			<view class="number">230</view>
			<view class="name">
				<image src="../../static/images/about-icon1.png" mode=""></image>
				信誉分
			</view>
		</view>
		<view class="xyuContLis">
			<view class="item">
				<view class="left">
					<view class="tit font28">产品名称：产品名称标题标题标题标题标题</view>
					<view class="data font24">2019.7.29</view>
				</view>
				<view class="right">-3</view>
			</view>
			<view class="item">
				<view class="left">
					<view class="tit font28">产品名称：产品名称标题标题标题标题标题</view>
					<view class="data font24">2019.7.29</view>
				</view>
				<view class="right">-3</view>
			</view>
			<view class="item">
				<view class="left">
					<view class="tit font28">产品名称：产品名称标题标题标题标题标题</view>
					<view class="data font24">2019.7.29</view>
				</view>
				<view class="right">-3</view>
			</view>
			<view class="item">
				<view class="left">
					<view class="tit font28">产品名称：产品名称标题标题标题标题标题</view>
					<view class="data font24">2019.7.29</view>
				</view>
				<view class="right">-3</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				webSelf: this,
				whether:false,
                num:0
			} 	
		},

		onLoad(options) {
	
		},
		
		onShow() {
			const self = this;
			document.title = '信誉分'			
		},

		methods: {		
		}
	}
</script>

<style>
.topCont{ width: 100%; height: 360rpx;background: #40b0ff;color: #FFFFFF;box-sizing: border-box;padding: 100rpx 0; text-align: center;}
.topCont .number{ font-size: 110rpx; line-height: 1;}
.topCont .name{ line-height: 40rpx; font-size: 30rpx;padding-top: 36rpx;;}
.topCont .name image{ display: inline-block; width: 34rpx; height:30rpx ;margin-right: 10rpx; vertical-align: middle;}

.xyuContLis .item{ padding:36rpx 3%; overflow: hidden; height: 150rpx; border-bottom: 2rpx solid #e1e1e1;box-sizing: border-box;}

.xyuContLis .left{ width: 80%;float: left;}
.xyuContLis .left .tit{ width: 100%; height: 30rpx; line-height: 30rpx; overflow: hidden;text-overflow: ellipsis;white-space: normal; font-size: 30rpx; ;}
.xyuContLis .left .data{ color: #999; font-size: 26rpx;padding-top: 12rpx;}
.xyuContLis .right{ width: 20%; float: right; color: #ff5050; font-size: 34rpx; text-align: right;height: 100%; padding-top: 20rpx; box-sizing: border-box;}


</style>
