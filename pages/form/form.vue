<template>
	<view class="container">
		<view class="formLis name-container">
			<view class="title">产品名称</view>
			<input v-model="submitData.title" type="text" placeholder="请输入产品名称" placeholder-style="color:#999999;font-size:28rpx;" />
		</view>

		<view class="formLis cate-container">
			<view class="title">交易类型</view>
			<view class="lable-selt">
				<radio-group class="radio-group"  @change="radioChange($event,'type')">
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

		<view class="formLis rolle-container">
			<view class="title">选择我的角色</view>
			<view class="lable-selt">
				<radio-group class="radio-group" @change="radioChange($event,'role')">
					<label>
						<radio class="selt" value="1" checked="checked"/>甲方
					</label>
					<label for="">
						<radio class="selt" value="2" />乙方
					</label>
				</radio-group>
			</view>
		</view>

		<view class="formLis tel-container" style="padding-top: 10rpx;padding-right: 120rpx;">
			<view class="title">交易对方手机号码</view>
				<input class="test" v-model="submitData.phone" type="number" placeholder="请输入对方手机号" maxlength="11" placeholder-style=" color:#999999;font-size:28rpx;" style="width:320rpx;text-align: right;"/>
			<view class="button" v-if="!other.user_no" @click="searchOther"><button>提交</button></view>
		</view>

		<view class="formLis phone-big-container" v-if="other.user_no" style="height: 70rpx;padding-bottom: 14rpx;margin-top: -10rpx; background: #fff;">
			
			<view>姓名:{{other.login_name}}</view>
			<view class="score">信用分:{{other.score}}</view>
			<view>已完结交易单数:{{other.total_count}}</view>
			
			<!-- <view class="phone-container">
				<view class="title">交易对方手机号</view>
				<view>18223025225</view>
			</view> -->
		</view>

		<view class="formLis sum-container">
			<view class="title">交易金额</view>
			<input v-model="submitData.price" type="number" placeholder="请输入交易金额" placeholder-style="color:#999999;font-size:13px;" />
		</view>

		<view class="formLis name-container">
			<view class="title">交易内容</view>
			<!-- <input v-model="submitData.content" type="text" placeholder="不刷量,不分销" placeholder-style="color:#000;font-size:13px;" /> -->
			<view class="jynr">不刷量，不分销</view>
		</view>

		<view class="formLis tip-container" style="height: 260rpx; justify-content: end; align-items: initial;padding-top: 20rpx;">
			<view class="title" style="margin-right: 20rpx;">增加内容</view>
			<textarea v-model="submitData.content" type="text" placeholder="请输入您要补充的信息" placeholder-style="color:#999999;font-size:13px;" />
		</view>
	   
	   
	<view class="formLis img-container" style="height: auto;border-bottom: none;justify-content: end; align-items: initial;padding-top: 20rpx;">
		<view class="title" style="width:120rpx;margin-right: 20rpx;">附件</view>
		<!-- <input type="file"  id="custom-up" @change='upload' style='display: none !important;'> -->
	  
		<view style="width:540rpx;">
			<view ref="input" class="input" style="display: none;"></view> 
			<view style="display:flex;align-items:center;justify-content: space-between;">
				<view class="text-container">
					<view>可上传图片或者文件</view>
					<view>上传点击无效请点击右上角复制链接，用其他手机浏览器打开</view>
					<view style="color: red;font-weight: bold;">(可上传多张)</view>
				</view>
				<!-- 客服二维码 -->
				<view class="code-container" @click="show()">
					<view>客服二维码</view>
					<image src="../../static/images/form-img1.png"/>
				</view>
			</view>
			<view>
				<image class="uploadBtn" @click="webSelf.$Utils.stopMultiClick(upload)" src="../../static/images/form-icon3.png" style="width:60rpx;height:60rpx;"/>
			</view>
			
			<!-- 上传显示的文件和图片 -->
			<view class="addImgbox">
				<template v-for="item in submitData.mainImg">
					<image :key="item.id" v-if="item.type=='image'" :src="item.url"></image>
					<view class="fileBox" :key="item.id" v-else >{{item.name}}</view>
				</template>
			</view>
		</view>
	  
	</view>
	
	<view class="submit" @click="webSelf.$Utils.stopMultiClick(submit)"><button>提交</button></view>
	
	<!-- 客服二维码弹窗 -->
	<view id="modal-bg" v-if="isShow"></view>
	<view id="modal" v-if="isShow">
		<view class="title">客服二维码</view>
		<image src="../../static/images/form-img1.png" class="code"/>
		<image src="../../static/images/about-icon8.png" id="close" @click="show()"/>
	</view>
	<!-- 客服二维码弹窗 -->
	<div id='showinfo'></div>
    <br />
    <div id='progress' style='display:none;text-align:center;'>
       <div id='bar' style='text-align:right;'></div>
    </div>

	
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
	
	<cUpload @uploadAfter="uploadAfter" ref="cUpload" ></cUpload>
</view>
</template>

<script>
	import cUpload from "@/components/upload/upload.vue"
	export default {
		components: {
			cUpload
		},
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
					role:'1',
					partner_no:''
				},
				other:{
					login_name:'',
					score:'100',
					total_count:'0',
					user_no:''
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
				searchOther(){
					const self = this;
					if(!self.submitData.phone){
						uni.showToast({
							title: '手机号未填写',
							duration: 1000,
							complete:function(){
								
							}
						});
						return;
					};
					if(self.submitData.phone==uni.getStorageSync('user_info').info.phone){
						uni.showToast({
							title: '不能填写自己手机号',
							duration: 1000,
							complete:function(){
								
							}
						});
						self.submitData.phone = '';
						return;
					};
					const postData = {
						tokenFuncName:'getProjectToken',
						searchItem:{
							phone:self.submitData.phone,
							user_type:0
						},
						getAfter:{
							User: {
								tableName: 'User',
								middleKey: 'user_no',
								key: 'user_no',
								condition: '=',
								info:['login_name'],
								searchItem: {
									status: 1,
								}
							},
							pCount:{
								tableName:'Project',
								middleKey:'user_no',
								key:'user_no',
								condition:'=',
								searchItem:{
									status:1
								},
								compute:{
									total_count:[
									  'count',
									  'status',
									  {
										status:1,
									  }
									],
								}
							}
						}
					};
					const callback = (res)=>{
						if(res.solely_code==100000){
							console.log('res',res)
							if(res.info.data.length>0){
								self.other.login_name = res.info.data[0]['User']['login_name'];
								self.other.total_count = res.info.data[0]['pCount']['total_count'];
								self.other.score = res.info.data[0]['score'];
								self.other.user_no = res.info.data[0]['user_no'];
								self.submitData.partner_no = self.other.user_no;
							}else{
								uni.showToast({
									title: '手机号未注册',
									duration: 1000,
									success:function(){
										
									}
								});
							};
						}else{
							uni.showToast({
								title: '网络故障',
								duration: 1000,
								success:function(){
									uni.setStorageSync('canClick', true);
								}
							});
						}
					};
					self.$apis.userInfoGet(postData, callback);
				},
			
				radioChange(e,key){
					console.log('e',e);
					console.log('key',key);
					const self = this;
					self.submitData[key] = e.target.value;
				},
			
				submit(){
					const self = this;
					//var pass = self.$Utils.checkComplete(self.submitData);
					//console.log('pass',pass);
					console.log('self.submitData',self.submitData)
					//if(pass){
						if(!self.other.user_no){
							uni.showToast({
								title: '请提交对方号码',
								duration: 1000,
								complete:function(){
									uni.setStorageSync('canClick', true);
								}
							});
							return;
						};
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
											self.$Router.navigateTo({route:{path:'/pages/myCenter/myCenter'}})
										},1000)
										
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
					//};
					self.$apis.projectAdd(postData, callback);
					console.log('self.submitData',self.submitData);
				},
			
				upload(){
					const self = this;
					self.$refs.cUpload.customButtonClick();
				},
				uploadAfter(res){
					const self = this;
					uni.setStorageSync('canClick', true);
					self.submitData.mainImg.push(res);
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
	.lable-selt{ position: absolute; right: 5%;}
	.lable-selt .selt{ width:60rpx; height:60rpx; font-size: 24rpx;}
	.lable-selt label{ font-size: 26rpx; padding-left: 20rpx;}
	/* uni-radio .uni-radio-input{width:10rpx!important;height:10rpx!important;} */
	.lable-selt uni-label{padding-left: 30rpx;}
</style>
