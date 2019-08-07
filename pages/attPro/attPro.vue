<template>
	<view class="attPro-container">
	   <view class="banner-container" :class="{fixTitle:whether}">
			<view @click="num=0" :class="{'active-item':num===0}"  class="item"><view class="text">进行中</view></view>
			<view @click="num=1" :class="{'active-item':num===1}"  class="item"><view class="text">已完结</view></view>
		</view>
		<view class="tab-con">
			<view class="tip-big-container" >
				<view class="tip-container" v-for="item in mainData"   @click="webSelf.$Router.navigateTo({route:{path:'/pages/proDetails/proDetails?project_no='+item.project_no}})">
					<view class="tip">
						<image src="../../static/images/canyu-icon3.png"/>
						<view class="title">产品名称：</view>
						<view class="name">{{item.title}}</view>
					</view>
					
					<view class="tip">
						<image src="../../static/images/canyu-icon4.png"/>
						<view class="title">交易类型：</view>
						<view class="name">{{item.type==1?'cpa':(item.type==2?'cps':'uv')}}</view>
						<view class="arrow"></view>
					</view>
					
					<view class="tip">
						<image src="../../static/images/canyu-icon5.png"/>
						<view class="title">我的角色：</view>
						<view class="name">{{item.Role.role==1?'甲方':'乙方'}}</view>
					</view>
					<view>
						<image class="fxdIcon" src="../../static/images/canyu-icon2.png" mode=""></image>
					</view>
					<view class="finishBtn" v-if="searchItem.step==1&&item.Role.role==1">
						<button type="button">完结</button>
					</view>
				</view>  
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
				mainData:[],
				paginate:{},
				isLoadAll:false,
				searchItem:{
					step:1
				}
			}
		},

		onLoad(options) {
			const self = this;
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		onShow() {
			const self = this;
			document.title = '参与项目';
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.mainData = [];
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		onReachBottom(){
			console.log('onReachBottom')
			const self = this;
			if(!self.isLoadAll&&uni.getStorageSync('canClick')){
				self.paginate.currentPage++;
				self.getMainData()
			};	
		},

		methods: {
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
			},
									
			getMainData(isNew) {
				const self = this;
				if(isNew){
					self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
					self.mainData = [];
				};
				const postData = {
					tokenFuncName:'getProjectToken',
					searchItem:self.$Utils.cloneForm(self.searchItem),
					paginate: self.$Utils.cloneForm(self.paginate)
				};
				postData.getAfter = {
					Role: {
						tableName: 'Relation',
						middleKey: 'user_no',
						key: 'relation_two',
						condition: '=',
						info:['role'],
						searchItem: {
							status: 1,
						}
					}
				};
				
				const callback = (res)=>{
					if(res.solely_code==100000){
						if(res.info.data.length>0){
							self.mainData.push.apply(self.mainData,res.info.data);
						}else{
							self.isLoadAll = true;
							uni.showToast({
								title: '没有更多了',
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
			}
		},

	}
</script>

<style>
	@import "../../assets/style/attPro.css";
	.finishBtn {overflow: hidden;}
	.finishBtn button{ width:120rpx; height:50rpx; text-align: center; line-height:50rpx; color: #00A1E9; border-radius: 8rpx; border: 1px solid #00A1E9; font-size: 26rpx; float: right; margin-right: 20rpx;}
</style>
