<template>
	<view class="attPro-container">
		<view class="banner-container" :class="{fixTitle:whether}">
			<view @click="num=0" :class="{'active-item':num===0}" class="item">
				<view class="text">详情</view>
			</view>
			<view @click="num=1" :class="{'active-item':num===1}" class="item">
				<view class="text">动态</view>
			</view>
		</view>
		<view class="tab-con">
			<view v-if="num===0">
				<view class="container">
					<view class="name-container formLis">
						<view class="title">产品名称</view>
						<input v-model="mainData.title" type="text" disabled="true"  placeholder-style="color:rgb(34,34,34);font-size:13px;" />
					</view>

					<view class="cate-container formLis">
						<view class="title">交易类型</view>
						{{mainData.type==1?'cpa':(mainData.type==2?'cps':'uv')}}
					</view>

					<view class="rolle-container formLis">
						<view class="title">选择我的角色</view>
						<view class="r_cont">
							{{mainData.Role&&mainData.Role.role==1?'甲方':'乙方'}}
						</view>
					</view>

					<view class="phone-big-container">
						<view class="phone-container formLis" style="border-bottom:none; height: 76rpx;padding-top: 10rpx;">
							<view class="title">交易对方手机号</view>
							<view class="r_cont">
								{{mainData.phone}}
							</view>
						</view>
						<view class="info-container formLis" style="height: 76rpx;padding-bottom: 10rpx;">
							<view><text>姓名:</text>{{mainData.User&&mainData.User.login_name}}</view>
							<view class="score"><text>信用分:</text>{{mainData.UserInfo&&mainData.UserInfo.score}}</view>
							<view><text>已完结交易单数:</text>{{mainData.pCount&&mainData.pCount.total_count}}</view>
						</view>
					</view>

					<view class="sum-container formLis">
						<view class="title">交易金额</view>
						<view class="r_cont">
							{{mainData.price}}
						</view>
					</view>

					<view class="name-container formLis">
						<view class="title">交易内容</view>
						<view class="r_cont">
							不刷量,不分销
						</view>
					</view>

					<view class="tip-container formLis" style="height: auto; justify-content: end; align-items: initial;padding-top: 20rpx;padding-bottom: 20rpx; ">
						<view class="title" style="margin-right: 40rpx;">增加内容</view>
						<view class="r_cont" style="width:480rpx;height:auto;padding:20rpx;background-color:#f5f5f5;flex-wrap: wrap;text-align: right;">
							<input v-model="mainData.content" :disabled="mainData.comfirm==0&&mainData.user_no!=myUserNo?false:true" type="text" value="" />
						</view>
					</view>
	   	<view class="img-container formLis" style="height: auto;padding-top: 20rpx;padding-bottom: 20rpx;">
					<view class="title">附件</view>
					<view class="img-little-container">
						<template v-for="item in mainData.mainImg" >
							<image :key="item.id" v-if="item.type=='image'" :src="item.url"></image>
							<view @click="downLoad(item.url)" :key="item.id" v-else >{{item.name}}</view>
						</template>
					</view>
				</view>
		
				<view class="flat-info" v-if="mainData.Role&&mainData.Role.role==1">
					<view class="phone-big-container">
						<view class="pTtitle">平台信息</view>
						<view class="info-container formLis">
							<view>付款账号</view>
							<view class="r_cont">{{thirdInfo.account}}</view>
						</view>
					</view>
					
					<view class="phone-container formLis" style="border-bottom:1px solid #F1F1F1;">
						<view class="title">姓名</view>
						<view class="r_cont">{{thirdInfo.name}}</view>
					</view>
				</view>
	   	
				<view class="button-big-container">
					<view class="button-container" v-if="mainData.comfirm==1">
						
						<view v-if="mainData.step!=2&&mainData.arbitration_step==0" class="button" @click="webSelf.$Router.navigateTo({route:{path:'/pages/applyArbitral/applyArbitral?project_no='+project_no+'&role'+mainData.Role.role}})"><button>申请仲裁</button></view>
						<view v-if="mainData.step!=2&&mainData.Role&&mainData.Role.role==1" class="button" @click="webSelf.$Router.navigateTo({route:{path:'/pages/voucher/voucher?project_no='+project_no+'&role'+mainData.Role.role}})"><button>上传付款凭证</button></view>
						<view v-if="mainData.step!=2&&mainData.Role&&mainData.Role.role==2" class="button" @click="webSelf.$Router.navigateTo({route:{path:'/pages/applyPay/applyPay?project_no='+project_no+'&role'+mainData.Role.role}})"><button>申请付款</button></view>
					</view>
					<view class="button-container" v-if="mainData.comfirm==0&&mainData.user_no!=myUserNo">
						<view  class="button" @click="confirm"><button>确认</button></view>
					</view>
					<view class="platform" @click="webSelf.$Router.navigateTo({route:{path:'/pages/article/article?title=平台说明'}})">
					  <image src="../../static/images/apply-icon5.png"/>《平台说明》
					  <!-- <text></text> -->
				   </view>
				</view>
			</view>
	   </view>
	  
	   <!-- 弹窗 -->
	  <!-- <view id="modal-bg" v-if="isShow"></view> -->
	 <!--  <view id="modal" > -->
	   <!-- 	<view class="title" >平台说明</view> -->
	   <!-- 	<image src="../../static/images/form-img1.png" class="code"/>
	   	<image src="../../static/images/about-icon8.png" id="close" @click="show()"/>
	   </view> -->
	   <!-- 弹窗 -->
	   
	</view>
	<view v-if="num===1">
	   <!--项目动态 -->
	     <view class="dynamic-big-container"> 
			 <view class="dynamic-container" style="height: 100%;" v-for="(item,index) in messageData" :key="index">
				 <view class="date-container">
					 <view class="jia">{{item.Role.role==1?'甲方':'乙方'}}</view>
					 <view class="date">{{item.create_time}}</view>
				 </view>
				 <view class="content">{{item.content}}</view>
				 <view class="addImgbox">
					<template v-for="c_item in item.mainImg" >
					 	<image :key="c_item.id" v-if="c_item.type=='image'" :src="c_item.url"></image>
					 	<view class="fileBox" :key="c_item.id" v-else >{{c_item.name}}</view>
					</template>
				 </view>
			</view>
			<view class="button" @click="webSelf.$Router.navigateTo({route:{path:'/pages/addDynamic/addDynamic?project_no='+project_no+'&role'+mainData.Role.role}})"><button>添加动态</button></view>
		 </view>
	   <!--项目动态 -->
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
                num:0,
				isShow:false,
				project_no:'',
				mainData:{},
				thirdInfo:{
					name:'',
					account:''
				},
				messageData:[],
				paginate:{},
				myUserNo:''
			}
		},

		onLoad(options) {
			const self = this;
			self.project_no = options.project_no;
			self.myUserNo = uni.getStorageSync('user_info').user_no;
			self.thirdInfo.name = uni.getStorageSync('user_info').thirdApp.name;
			self.thirdInfo.account = uni.getStorageSync('user_info').thirdApp.account;
			
			
		},
		
		onShow() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.messageData = [];
			self.$Utils.loadAll(['getMainData','getProcessData'], self);
		},
		
		onReachBottom(){
			console.log('onReachBottom')
			const self = this;
			if(self.num==1&&!self.isLoadAll&&uni.getStorageSync('canClick')){
				self.paginate.currentPage++;
				self.getProcessData()
			};	
		},


		methods: {
			
			test(){
				
			},
			
			
			confirm(){
			
				const self = this;
				const postData = {
					tokenFuncName:'getProjectToken',
					searchItem:{
						project_no:self.project_no,
						user_no:self.mainData.user_no,
					},
					data:{
						comfirm:1,
						content:self.mainData.content
					}
				};
				const callback = (res)=>{
					if(res.solely_code==100000){
						uni.showToast({
							title: '确认成功',
							duration: 1000,
							success:function(){
								
							}
						});
						self.getMainData();
					}else{
						uni.showToast({
							title: '确认失败',
							duration: 1000,
							success:function(){
								
							}
						});
					};
				};
				self.$apis.projectUpdate(postData, callback);
			},
			
			downLoad(url){
				window.open(url)
			},
			
			getMainData() {
				const self = this;
				const postData = {
					tokenFuncName:'getProjectToken',
					searchItem:{
						project_no:self.project_no
					},
					getAfter:{
						
						UserInfo:{
							tableName: 'UserInfo',
							middleKey: 'phone',
							key: 'phone',
							condition: '=',
							info:['score','user_no'],
							searchItem: {
								status: 1,
								user_type:0
							}
						},
						User: {
							tableName: 'User',
							middleKey: ['UserInfo','user_no'],
							key: 'user_no',
							condition: '=',
							info:['login_name'],
							searchItem: {
								status: 1,
							}
						},
						pCount:{
							tableName:'Project',
							middleKey: ['UserInfo','user_no'],
							key:'user_no',
							condition:'=',
							searchItem:{
								status:1,
								step:2
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
						},
						
						Role: {
							tableName: 'Relation',
							middleKey: 'status',
							key: 'status',
							condition: '=',
							info:['role'],
							searchItem: {
								relation_two:uni.getStorageSync('user_info').user_no,
								relation_one:self.project_no
							}
						}
					},
					
				};

				
				const callback = (res)=>{
					if(res.solely_code==100000){
						if(res.info.data.length>0){
							self.mainData = res.info.data[0];
						}else{
							uni.showToast({
								title: 'id有误',
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
							}
						});
					};
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.projectGet(postData, callback);
				
			},
			
			getProcessData(isNew){
				const self = this;
				if(isNew){
					self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
					self.messageData = [];
				};
				const postData = {
					searchItem:{
						project_no:self.project_no,
						type:1,
						user_type:0
					},
					paginate:self.$Utils.cloneForm(self.paginate),
					getAfter:{
						Role: {
							tableName: 'Relation',
							middleKey: 'user_no',
							key: 'relation_two',
							condition: '=',
							info:['role'],
							searchItem: {
								relation_one:self.project_no
							}
						}
					}
				};
				const callback = (res)=>{
					if(res.solely_code==100000){
						if(res.info.data.length>0){
							self.messageData.push.apply(self.messageData, res.info.data);	
						}else{
							self.isLoadAll = true;
							uni.showToast({
								title: '没有更多了',
								duration: 1000,
								success:function(){
									
								}
							});
						}
					}else{
						uni.showToast({
							title: '网络故障',
							duration: 1000,
							success:function(){
								
							}
						});
					};
					self.$Utils.finishFunc('getProcessData');
				};
				self.$apis.processGet(postData, callback);
			},

			show() {
				const self = this;
				
				self.isShow = !self.isShow
			},


			menuChange(num) {
				const self = this;
				self.num = num;
			}						
		},
	
	}
</script>

<style>
	@import "../../assets/style/proDetails.css";
</style>
