<template>
	<view class="myCtfcation">
		<view class="item-lis">
			<view class="tit">收款人姓名：</view>
			<input class="write" type="text" placeholder="请输入收款人姓名">
		</view>
		<view class="item-lis">
			<view class="tit">开户行：</view>
			<input class="write" type="text" placeholder="请输入银行的开户行">
		</view>
		<view class="item-lis" style="padding-left: 220rpx;">
			<view class="tit" style="width:220rpx">收款银行卡号：</view>
			<input class="write" type="text" placeholder="请输入收款账号">
		</view>
		
		<view><button  class="okBtn">提交</button></view>
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
			document.title = '实名认证'			
		},

		methods: {		
		}
	}
</script>

<style>
	.myCtfcation{padding:0 3%;}
	.item-lis{padding:40rpx 0; line-height: 60rpx; position: relative; padding-left: 180rpx;border-bottom: 2rpx solid #e1e1e1;}
	.item-lis .tit{font-size: 28rpx; width: 180rpx; float:left; position: absolute;left: 0; top:40rpx;}
	.item-lis .write{ width: 100%; height: 60rpx;background: #f6f6f6;padding: 0 20rpx; box-sizing: border-box; font-size: 26rpx;}
	.okBtn{  width: 80%; height: 80rpx;color: #ffffff; background-color: rgb(3,150,255); font-size: 30rpx; line-height: 80rpx; margin:280rpx auto 100rpx auto;}
</style>
