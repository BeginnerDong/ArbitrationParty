<template>
<view class="container">
	<view class="nickname-container">
		<image class="photo" :src="wx_info.hedaImgUrl?wx_info.hedaImgUrl:'../../static/images/about-img.png'"/>
		<view class="nickname-img">
			<view class="nickname">{{login_name}}</view>
			<view class="score">
				<image src="../../static/images/about-icon1.png"/>
				<text>信誉分:{{score}}</text>
			</view>
		</view>
	</view>
	<view class="project-big-container">
		<view class="project-container">
			<!--一个item-->
			  <view class="item"  @click="webSelf.$Router.navigateTo({route:{path:'/pages/form/form'}})">
			 	 <view><image src="../../static/images/about-icon2.png"/></view>
			 	 <view class="text"><text>创建项目</text></view>
			 </view>
			<!--一个item-->
			
			<!--一个item-->
			  <view class="item"   @click="webSelf.$Router.navigateTo({route:{path:'/pages/attPro/attPro'}})">
			 	 <view><image src="../../static/images/about-icon3.png"/></view>
			 	 <view class="text"><text>参与项目</text></view>
			  </view>
			<!--一个item-->
			
			<!--一个item-->
			  <view class="item" @click="webSelf.$Router.navigateTo({route:{path:'/pages/myArbitral/myArbitral'}})">
			 	 <view><image src="../../static/images/about-icon4.png"/></view>
			 	 <view class="text"><text>我的仲裁</text></view>
			 </view>
			<!--一个item-->
			
			<!--一个item-->
			  <view class="item"  @click="webSelf.$Router.navigateTo({route:{path:'/pages/myTrading/myTrading'}})">
			 	 <view><image src="../../static/images/about-icon5.png"/></view>
			 	 <view class="text">交易流水</view>
			 </view>
			<!--一个item-->
			
			<!--一个item-->
			  <view class="item"  @click="webSelf.$Router.navigateTo({route:{path:'/pages/myCtfcation/myCtfcation'}})">
			 	 <view><image src="../../static/images/about-icon6.png"/></view>
			 	 <view class="text">实名认证</view>
			 </view>
			<!--一个item-->
			
			<!--一个item-->
			  <view class="item" @click="webSelf.$Router.navigateTo({route:{path:'/pages/myCredit/myCredit'}})">
			 	 <view><image src="../../static/images/about-icon7.png"/></view>
			 	 <view class="text">信誉分</view>
			 </view>
			<!--一个item-->
		</view>
	</view>
	<!--浮窗 -->
	<view class="float-container" @click="showAlert"><text>加入浮窗</text></view>
	<!--浮窗-->
	<view class="alertFcBox" v-if="showView">
		<img class="bjpic" src="../../static/images/about-icon9.png" alt="">
		<view>
			<img class="closeBtn" @click="coloseAlert"  src="../../static/images/about-wicon8.png" alt="">
		</view>
	</view>
	
	<!-- 弹窗 -->
	<!-- <view id="modal-bg">
		
	</view>
	<view id="modal">
		<image src="../../static/images/about-icon9.png" class="code"/>
		<image src="../../static/images/about-icon8.png" id="close"/>
		<text>点击上方,加入浮窗</text>
	</view> -->
	<!-- 弹窗 -->
	
	<!--底部tab键-->
	<view class="navbar">
		<view class="navbar_item"  @click="webSelf.$Router.navigateTo({route:{path:'/pages/form/form'}})">
			<view class="nav_img">
				<image src="../../static/images/nabar1.png"/>
			</view>
			<view class="text">表单</view>
		</view>
		<view class="navbar_item" @click="webSelf.$Router.navigateTo({route:{path:'/pages/myCenter/myCenter'}})">
			<view class="nav_img">
				<image src="../../static/images/nabar2-a.png"/>
			</view>
			<view class="text this-text">我的</view>
		</view>		
	</view>
	<!--底部tab键-->
</view>

</template>

<script>
	export default {
		data() {
			return {
				webSelf: this,
				showView: false,
				score:'',
				login_name:'',
				wx_info:{}
			}
		},

		onLoad(options) {
			const self = this;
			self.score = uni.getStorageSync('user_info').info.score;
			self.login_name = uni.getStorageSync('user_info').login_name;
			/* var ua = navigator.userAgent.toLowerCase();//获取判断用的对象
			if (ua.match(/MicroMessenger/i) == "micromessenger") {
					var wx_info_expire_time = uni.getStorageSync('wx_info_expire_time');
					var wx_info = uni.getStorageSync('wx_info');
					if(!wx_info||wx_info_expire_time<(new Date()).getTime()){
						self.$Token.getWeixinToken();
					}else{
						self.wx_info = wx_info;
					};
			}; */

		},
		
		onShow() {
			const self = this;
			document.title = '个人中心'			
		},


		methods: {
			showAlert(){
				this.showView = true;
			},
			coloseAlert(){
				this.showView = false;
			},
			isShow() {
				const self = this;
				self.is_show_this = !self.is_show_this;
				if(self.num==0){
					self.left = self.left+1
				}else if(self.num==1){
					self.right = self.right+1
				}
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
	@import "../../assets/style/myCenter.css";
	@import "../../assets/style/common.css";
	
	.alertFcBox{ position: fixed; top:0; right: 0; bottom: 0; left: 0;background: rgba(0,0,0,0.5);  z-index: 9999; padding-top: 120rpx;}
	.alertFcBox .bjpic{ width: 80%;margin: 0 auto; display: block;}
	.alertFcBox .closeBtn{ width: 60rpx; height: 60rpx; display: block; margin: 100rpx auto; padding: 50rpx; cursor: pointer;}

	.bdm {
		-webkit-animation: updanmu 4s linear;
		animation: updanmu 4s linear;
	}

	@-webkit-keyframes updanmu {
		0% {
			-webkit-transform: translateY(120px);
			opacity: 0
		}

		25% {
			-webkit-transform: translateY(90px);
			opacity: 1
		}

		50% {
			-webkit-transform: translateY(60px);
			opacity: 1
		}

		75% {
			-webkit-transform: translateY(30px);
			opacity: 1
		}

		100% {
			-webkit-transform: translateY(0);
			opacity: 0
		}
	}

	@keyframes updanmu {
		0% {
			transform: translateY(120px);
			opacity: 0
		}

		25% {
			transform: translateY(90px);
			opacity: 1
		}

		50% {
			transform: translateY(60px);
			opacity: 1
		}

		75% {
			transform: translateY(30px);
			opacity: 1
		}

		100% {
			transform: translateY(0);
			opacity: 0
		}
	}
</style>
