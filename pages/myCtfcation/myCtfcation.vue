<template>
	<view class="myCtfcation">
		<view class="item-lis">
			<view class="tit">收款人姓名：</view>
			<input v-model="submitData.name" class="write" type="text" placeholder="请输入收款人姓名">
		</view>
		<view class="item-lis">
			<view class="tit">开户行：</view>
			<input v-model="submitData.bank" class="write" type="text" placeholder="请输入银行的开户行">
		</view>
		<view class="item-lis" style="padding-left: 220rpx;">
			<view class="tit" style="width:220rpx">收款银行卡号：</view>
			<input v-model="submitData.idCard" class="write" type="text" placeholder="请输入收款账号">
		</view>
		
		<view>
			<button  class="okBtn" @click="webSelf.$Utils.stopMultiClick(submit)" >提交</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				webSelf: this,
				whether:false,
                num:0,
				submitData:{
					bank:'',
					idCard:'',
					name:''
				}
			} 	
		},
		
		onLoad(options) {
			const self = this;
			uni.setStorageSync('canClick', true);
			self.$Utils.loadAll(['getUserInfo'], self);
		},
		
		onShow() {
			const self = this;
			document.title = '实名认证'			
		},
		
		methods: {	
			getUserInfo(){
				const self = this;
				const postData = {
					tokenFuncName:'getProjectToken',
					searchItem:{
						user_no:uni.getStorageSync('user_info').user_no
					}
				};
				const callback = (res)=>{
					if(res.solely_code==100000){
						if(res.info.data.length>0){
							self.submitData.bank = res.info.data[0].bank;
							self.submitData.idCard = res.info.data[0].idCard;
							self.submitData.name = res.info.data[0].name;
							
						}else{
							uni.showToast({
								title: '无数据',
								duration: 1000,
								complete:function(){
								}
							});
						}
		
					}else{
						uni.showToast({
							title: res.msg,
							duration: 1000,
							complete:function(){
							}
						});
					};
					self.$Utils.finishFunc('getUserInfo');
				};
				self.$apis.userInfoGet(postData, callback);
			},
			submit(){
				const self = this;
				const postData = {
					tokenFuncName:'getProjectToken',
					data:self.submitData
				};
				const callback = (res)=>{
					if(res.solely_code==100000){
						uni.showToast({
							title: '提交成功',
							duration: 1000,
							complete:function(){
								uni.setStorageSync('canClick', true);
								setTimeout(function(){
									uni.navigateBack({
										delta: 1
									});
								},1000);	
							}
						});
					}else{
						uni.showToast({
							title: '提交失败',
							duration: 1000,
							complete:function(){
								uni.setStorageSync('canClick', true);
							}
						});
					}
				};
				self.$apis.userInfoUpdate(postData, callback);
			}
		}
	}
</script>

<style>
	.myCtfcation{padding:0 3%;}
	.item-lis{padding:30rpx 0; line-height: 60rpx; position: relative; padding-left: 180rpx;border-bottom: 2rpx solid #e1e1e1;}
	.item-lis .tit{font-size: 30rpx; width: 180rpx; float:left; position: absolute;left: 0; top:50%; transform: translateY(-50%);}
	.item-lis .write{ width: 100%; height: 60rpx;background: #f6f6f6;padding: 0 20rpx; box-sizing: border-box; font-size: 30rpx;}
	.okBtn{  width: 80%; height: 80rpx;color: #ffffff; background-color: rgb(3,150,255); font-size: 30rpx; line-height: 80rpx; margin:280rpx auto 100rpx auto;}
</style>
