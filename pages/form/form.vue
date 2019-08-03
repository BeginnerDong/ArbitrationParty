<template>
	<view class="container">
		<view class="name-container">
			<view class="title">产品名称</view>
			<input v-model="submitData.title" type="text" placeholder="请输入产品名称" placeholder-style="color:#999999;font-size:13px;" />
		</view>

		<view class="cate-container">
			<view class="title">交易类型</view>
			<view class="lable-selt">
				<radio-group class="radio-group" bindchange="changeSex">
					<label>
						<radio  class="selt" name="type" value="1" checked="checked"/>cpa
					</label>
					<label for="">
						<radio class="selt" name="type" value="2" />cps
					</label>
					<label for="" style="width:20rpx;height:20rpx">
						<radio class="selt" name="type" value="3" />uv
					</label>
				</radio-group>
			</view>
		</view>

		<view class="rolle-container">
			<view class="title">选择我的角色</view>
			<view class="lable-selt">
				<radio-group class="radio-group" bindchange="changeSex">
					<label>
						<radio class="selt" value="1" checked="checked"/>甲方
					</label>
					<label for="">
						<radio class="selt" value="2" />乙方
					</label>
				</radio-group>
			</view>
		</view>

		<view class="tel-container">
			<view class="title" style="width:33%;">交易对方手机号</view>
			<input v-model="submitData.phone" type="number" style="width: 40%;" placeholder="请输入对方手机号" maxlength="11" placeholder-style="color:#999999;font-size:13px; width:100%;text-align: right; left:auto; right:0" />
			<view class="button"><button>提交</button></view>
		</view>

		<view class="phone-big-container">

			<view class="phone-container">
				<view class="title">交易对方手机号</view>
				<view>18223025225</view>
			</view>
			<view class="info-container">
				<view>姓名:张瑞</view>
				<view class="score">信用分:100</view>
				<view>已完结交易单数:5</view>
			</view>

		</view>

		<view class="sum-container">
			<view class="title">交易金额</view>
			<input v-model="submitData.price" type="number" placeholder="请输入交易金额" placeholder-style="color:#999999;font-size:13px;" />
		</view>

		<view class="name-container">
			<view class="title">交易内容</view>
			<!-- <input v-model="submitData.content" type="text" placeholder="不刷量,不分销" placeholder-style="color:#000;font-size:13px;" /> -->
			不刷量,不分销
		</view>

		<view class="tip-container">
			<view class="title">增加内容</view>
			<textarea v-model="submitData.content" type="text" placeholder="请输入您要补充的信息" placeholder-style="color:#999999;font-size:13px;" />
		</view>
	   
	   
	<view class="img-container">
	  <view class="title">附件</view>
	  <input type="file"  id="custom-up" @change='upload' style='display: none !important;'>
	  <image @click="webSelf.$Utils.stopMultiClick(customButtonClick)" src="../../static/images/form-icon3.png"/>
	  <view class="text-container">
		  <view><p>可上传图片或者文件</p></view>
		  <view><p class="p2">(可上传多张)</p></view>
	  </view>
	  <view v-for="item in submitData.mainImg">
		  <image :src="item.url"></image>
	  </view>
	  <view class="code-container" @click="show()">
		  <view>客服二维码</view>
		  <image src="../../static/images/form-img1.png"/>
	  </view>
	</view>
	
	<view class="submit"><button>提交</button></view>
	
	<!-- 客服二维码弹窗 -->
	<view id="modal-bg" v-if="isShow"></view>
	<view id="modal" v-if="isShow">
		<view class="title">客服二维码</view>
		<image src="../../static/images/form-img1.png" class="code"/>
		<image src="../../static/images/about-icon8.png" id="close" @click="show()"/>
	</view>
	<!-- 客服二维码弹窗 -->
	
	
	<!--底部tab键-->
	<view class="navbar">
		<view class="navbar_item"  @click="webSelf.$Router.navigateTo({route:{path:'/pages/form/form'}})">
			<view class="nav_img">
				<image src="../../static/images/nabar1-a.png"/>
			</view>
			<view class="text this-text">表单</view>
		</view>
		<view class="navbar_item" @click="webSelf.$Router.navigateTo({route:{path:'/pages/myCenter/myCenter'}})">
			<view class="nav_img">
				<image src="../../static/images/nabar2.png"/>
			</view>
			<view class="text">我的</view>
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
				isShow:false,
				submitData:{
					title:'',
					type:'1',
					price:'',
					phone:'',
					content:'',
					mainImg:[],
				}
			}
		},
	
		onLoad(options) {
			const self = this;
			uni.setStorageSync('canClick', true);
		},
		
		onShow() {
			const self = this;
			document.title = '提交表单'			
		},
		methods: {
				customButtonClick(){
				  const self = this;
				  console.log('996352',document.getElementById("custom-up"));
				  document.getElementById("custom-up").click();
				  
				},
				upload(){
					const self = this; 
					let file = e.target.files[0]
					console.log('file',file)
							
					uni.uploadFile({
						url: 'http://loan.52team.top/api/public/index.php/api/v1/Base/FtpFile/upload', //仅为示例，非真实的接口地址
						filePath: tempFilePaths[0],
						name: 'file',
						formData: {
							'token':uni.getStorageSync('user_token')
						},
						success: (uploadFileRes) => {
							
							if(res.solely_code==100000){
								self.submitData.mainImg.push(res.info);
								uni.setStorageSync('canClick', true);
							}else{
								uni.showToast({
									title: res.msg,
									duration: 2000,
									success:function(){
										uni.setStorageSync('canClick', true);
									}
								});
							};
							console.log(uploadFileRes.data);
						},
						complete:function(){
							uni.setStorageSync('canClick', true);
						}
					});
							
							
						
				},
		
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
	@import "../../assets/style/form.css";
	@import "../../assets/style/common.css";
	.lable-selt{ position: absolute; right: 40rpx;}
	.lable-selt .selt{ width:60rpx; height:60rpx; font-size: 24rpx;}
	.lable-selt label{ font-size: 26rpx; padding-left: 20rpx;}
	/* uni-radio .uni-radio-input{width:10rpx!important;height:10rpx!important;} */
	.lable-selt uni-label{padding-left: 30rpx;}
</style>
