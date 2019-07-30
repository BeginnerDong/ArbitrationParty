<template>
	<view class="container">
		<view class="name-container">
			<view class="title">申请金额：</view>
			<input type="text" placeholder="请输入申请金额" placeholder-style="color:#999999;font-size:12px;" />
		</view>
		
		<view class="name-container">
			<view class="title">手续费：</view>
			<input type="text" disabled="true" placeholder="￥500" placeholder-style="color:rgb(34,34,34);font-size:13px;" />
		</view>
		
		<view class="name-container">
			<view class="title">手续费承担方：</view>
			<view class="style-container">
			 <view class="style-little-container">
				<image src="../../static/images/form-icon1.png"/>
				<text>甲方</text>
			 </view>
			<view class="style-little-container">
				<image src="../../static/images/form-icon1.png"/>
				<text>乙方</text>
			</view>
			<view class="style-little-container">
				<image src="../../static/images/form-icon1.png"/>
				<text>双方平摊</text>
			</view>
		</view>
		</view>
		
		<view class="tip-container">
			<view class="title">申请理由:</view>
			<textarea type="text" placeholder="请输入您的申请理由" placeholder-style="color:#999999;font-size:11px;" />
		</view>
		<view class="tip-container">
			<view class="title">手续费：</view>
			<view class="right-uppic">
				<input type="file" placeholder-style="color:#999999;font-size:11px;"/>
				<image class="icon" src="../../static/images/form-icon3.png"/>
			</view>
			
		</view>

	
	<view class="submit"><button>确认</button></view>
	
	
	
</view>
</template>

<script>
	export default {
		data() {
			return {
				webSelf: this,
				isShow:false
			}
		},
	
		onLoad(options) {
	
		},
		
		onShow() {
			const self = this;
			document.title = '申请付款'			
		},
		methods: {
		
				show() {
					const self = this;
					
					self.isShow = !self.isShow
				},
		
				notice() {
					const self = this;
					self.$Utils.showToast('购买后可获得', 'none', 2000)
				},
		
				isOpen() {
					const self = this;
					self.is_open = true;
					console.log("self.is_open", self.is_open)
				},
		
				menuChange(num) {
					const self = this;
					self.num = num;
				},
				
				getProductData() {
					const self = this;
					const postData = {
						thirdapp_id: 2
					};
					console.log('postData', postData)
					const callback = (res) => {
						if (res.info.data.length > 0) {
							self.productData = res.info.data[0]
							
						}
						console.log('res', res)
						
						self.getCouponData()
					};
					self.$apis.productGet(postData, callback);
				},
		
				tokenGet() {
					const self = this;
					const postData = {
						searchItem: {
							user_no: 'U709654952588131'
						}
					};
					console.log('postData', postData)
					const callback = (res) => {
						if (res.solely_code == 100000) {
							uni.setStorageSync('user_token', res.token);
							uni.setStorageSync('user_no', res.info.user_no);
							uni.setStorageSync('user_info', res.info);
						}
						console.log('res', res)
						self.$Utils.finishFunc('tokenGet');
					};
					self.$apis.tokenGet(postData, callback);
				},
		
				getMainData() {
					const self = this;
					const postData = {};
					postData.tokenFuncName = 'getProjectToken';
					postData.searchItem = {
						thirdapp_id: self.$AssetsConfig.thirdapp_id,
						user_no: uni.getStorageSync('user_no')
					};
					postData.getAfter = {
						hasOrder: {
							tableName: 'Order',
							middleKey: 'user_no',
							key: 'user_no',
							condition: '=',
							searchItem: {
								status: 1,
								pay_status: 1
							}
						},
						hasCoupon: {
							tableName: 'UserCoupon',
							middleKey: 'user_no',
							key: 'user_no',
							condition: '=',
							searchItem: {
								status: 1,
								use_step: 1
							}
						},
					};
					const callback = (res) => {
						if (res.info.data.length > 0) {
							self.mainData = res.info.data[0];
							if (self.mainData.hasOrder.length == 0) {
								self.is_show = true;
								
							} else {
		
								self.$Router.redirectTo({
									route: {
										path: '/pages/todayread/todayread'
									}
								})
							}
						};
						self.$Utils.finishFunc('getMainData');
					};
					self.$apis.userGet(postData, callback);
				},
		
				getArticleOneData() {
					const self = this;
					const postData = {
						searchItem: {
							title: '计划介绍'
						}
					};
					const callback = (res) => {
						if (res.info.data.length > 0) {
							self.articleOneData = res.info.data[0]
						};
						self.$Utils.finishFunc('getArticleOneData');
					};
					self.$apis.articleGet(postData, callback);
				},
		
				getArticleTwoData() {
					const self = this;
					const postData = {
						searchItem: {
							title: '绘本书单'
						}
					};
					const callback = (res) => {
						if (res.info.data.length > 0) {
							self.articleTwoData = res.info.data[0]
						};
						self.$Utils.finishFunc('getArticleTwoData');
					};
					self.$apis.articleGet(postData, callback);
				},
		
		
				getMessageData() {
					const self = this;
					const postData = {
						searchItem: {
							type: 1,
						}
					};
					const callback = (res) => {
						if (res.solely_code == 100000) {
							if (res.info.data.length > 0) {
								self.messageData.push.apply(self.messageData, res.info.data);
								for (var i = 0; i < self.messageData.length; i++) {
									self.messageData[i].class = 'bdm';
									if (i > 0) {
										self.messageData[i].style = '-webkit-animation-delay: ' + (i * 2) + 's;animation-delay: ' + (i * 2) + 's';
									} else {
										self.messageData[i].style = '';
									};
								};
								console.log('self.messageData', self.messageData)
							};
							setInterval(function() {
								for (var i = 0; i < self.messageData.length; i++) {
									self.messageData[i].class = '';
								};
							}, self.messageData.length * 2000 + 4000)
							setInterval(function() {
								for (var i = 0; i < self.messageData.length; i++) {
									self.messageData[i].class = 'bdm';
								};
							}, self.messageData.length * 2000 + 5000)
						};
						self.$Utils.finishFunc('getMessageData');
					};
					self.$apis.messageGet(postData, callback);
				},
		
				getCouponData() {
					const self = this;
					const postData = {};
					const callback = (res) => {
						if (res.info.data.length > 0) {
							self.couponData = res.info.data[0]
							
							self.money  = (self.productData.price - self.couponData.discount).toFixed(2)
						};
						self.$Utils.finishFunc('getProductData');
					};
					self.$apis.couponGet(postData, callback);
				},
		
				couponAdd() {
					const self = this;
		
					const postData = {
						tokenFuncName: 'getProjectToken',
						coupon_id: self.couponData.id,
						data: {
							pay_status: 1,
						},
					};
					console.log('postData', postData)
					const callback = (res) => {
						if (res && res.solely_code == 100000) {
							self.$Utils.showToast('领取成功', 'none', 2000)
							self.mainData.hasCoupon.push({
								status: 1
							})
						} else {
							self.$Utils.showToast(res.msg, 'none')
						}
					};
					self.$apis.couponAdd(postData, callback);
				},
		
		
			}
		}
	
</script>

<style>
	@import "../../assets/style/applyPay.css";
	.right-uppic{width: 20%; height: 90px; padding: 4%; background-color: rgb(243,243,243); position: relative;}  
	.right-uppic input{ width: 100%; height: 100%; opacity: 0.5;}
	.right-uppic .icon{width:64rpx;height: 64rpx;position: absolute;left: 50%;top: 50%;transform: translate(-50%,-50%);}
	
</style>
