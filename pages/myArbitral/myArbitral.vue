<template>
	<view class="attPro-container">
	   <view class="banner-container" :class="{fixTitle:whether}">
			<view @click="changeNum(0)" :class="{'active-item':num===0}"  class="item"><view class="text">我参与的</view></view>
			<view @click="changeNum(1)" :class="{'active-item':num===1}"  class="item"><view class="text">全民仲裁</view></view>
		</view>
		<view class="tab-con">
			<view class="tip-big-container">
				<template v-for="item in mainData">
					<view class="tip-container"   @click="webSelf.$Router.navigateTo({route:{path:'/pages/myArbitralDetail/myArbitralDetail?project_no='+item.project_no}})">
						<view class="tip">
							<image src="../../static/images/canyu-icon3.png"/>
							<view class="title">产品名称：</view>
							<view class="name">{{item.title}}</view>
						</view>
						<view class="tip">
							<image src="../../static/images/canyu-icon4.png"/>
							<view class="title">交易类型：</view>
							<view class="name">{{item.type==1?'cpa':(item.type==2?'cps':'uv')}}</view>
						</view>
						<view class="tip">
							<image src="../../static/images/canyu-icon5.png"/>
							<view class="title">我的角色：</view>
							<view class="name">{{item.Role&&item.Role.role==1?'甲方':'乙方'}}</view>
						</view>
						<view class="fixedIcon">{{item.arbitration_type==1?'平台仲裁':'全民仲裁'}}</view>
					</view>
				</template>
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
				searchItem:{
					arbitration_step:1,
					deadline:['>',(new Date()).getTime()/1000]
				},
				mainData:[]
			}
		},

		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
		},
		
		onShow() {
			const self = this;
			self.$Utils.loadAll(['getMainData'], self);		
		},
		
		onReachBottom(){
			console.log('onReachBottom')
			const self = this;
			if(self.num==1&&!self.isLoadAll&&uni.getStorageSync('canClick')){
				self.paginate.currentPage++;
				self.getMainData()
			};	
		},


		methods: {
			
			changeNum(num){
				const self = this;
				if(self.num!=num){
					self.num = num;
					self.getMainData(true);
				};
			},
			
			
			getMainData(isNew){
				const self = this;
				if(isNew){
					self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
					self.mainData = [];
				};
				const postData = {
					tokenFuncName:'getProjectToken',
					searchItem:self.$Utils.cloneForm(self.searchItem),
					paginate : self.$Utils.cloneForm(self.paginate),
					getAfter:{
						Role: {
							tableName: 'Relation',
							middleKey: 'project_no',
							key: 'relation_one',
							condition: '=',
							info:['role'],
							searchItem: {
								relation_two:uni.getStorageSync('user_info').user_no,
							}
						}
					}
				};
				if(self.num==0){
					postData.getBefore = {
						spu: {
							tableName: 'Relation',
							middleKey: 'project_no',
							key: 'relation_one',
							searchItem: {
								relation_two:['in',[uni.getStorageSync('user_info').user_no]]
							},
							condition: 'in'
						}
					};
				};
				if(self.num==1){
					postData.searchItem.arbitration_type = 2;
				};
				const callback = (res)=>{
					if(res.solely_code==100000){
						if(res.info.data.length>0){
							self.mainData.push.apply(self.mainData, res.info.data);	
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
					self.$Utils.finishFunc('getMainData');
				};
				self.$apis.projectGet(postData, callback);
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


			menuChange(num) {
				const self = this;
				self.num = num;
			}						
	},
	
}
</script>

<style>
	@import "../../assets/style/myArbitral.css";
</style>
