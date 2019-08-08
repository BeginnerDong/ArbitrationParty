<template>
	<view class="myCreditbox">
		<view class="topCont center white">
			<view class="number">{{userInfo.score}}</view>
			<view class="name">
				<image src="../../static/images/about-icon1.png" mode=""></image>
				信誉分
			</view>
		</view>
		<view class="xyuContLis">
			<view class="item" v-for="item in mainData">
				<view class="left">
					<view class="tit font28">产品名称：{{item.Project.title}}</view>
					<view class="data font24">{{item.create_time}}</view>
				</view>
				<view class="right">{{item.count}}</view>
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
				userInfo:{},
				isLoadAll:false,
				paginate:{}
			} 	
		},

		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getUserInfo','getMainData'], self);
		},
		
		onShow() {
			const self = this;
			document.title = '信誉分'			
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
							self.userInfo = res.info.data[0];	
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
			getMainData(){
				const self = this;
				const postData = {
					tokenFuncName:'getProjectToken',
					paginate:self.$Utils.cloneForm(self.paginate),
					searchItem:{
						user_no:uni.getStorageSync('user_info').user_no,
						type:3,
					}
				};
				postData.getAfter = {
					Project: {
						tableName: 'Project',
						middleKey: 'project_no',
						key: 'project_no',
						condition: '=',
						info:['title'],
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
					setTimeout(function(){
						self.$Utils.finishFunc('getMainData');
					},1200);
				};
				self.$apis.flowLogGet(postData, callback);
			}
		}
	}
</script>

<style>
.topCont{ width: 100%; height: 360rpx;background: #40b0ff;color: #FFFFFF;box-sizing: border-box;padding: 100rpx 0; text-align: center;}
.topCont .number{ font-size: 110rpx; line-height: 1;}
.topCont .name{ line-height: 40rpx; font-size: 30rpx;padding-top: 36rpx;;}
.topCont .name image{ display: inline-block; width: 34rpx; height:30rpx ;margin-right: 10rpx; vertical-align: middle;}

.xyuContLis .item{ padding:30rpx 3%; overflow: hidden; height: 140rpx; border-bottom: 2rpx solid #e1e1e1;box-sizing: border-box;}

.xyuContLis .left{ width: 80%;float: left;}
.xyuContLis .left .tit{ width: 100%; height: 30rpx; line-height: 30rpx; overflow: hidden;text-overflow: ellipsis;white-space: normal; font-size: 30rpx; ;}
.xyuContLis .left .data{ color: #999; font-size: 26rpx;padding-top: 16rpx;}
.xyuContLis .right{ width: 20%; float: right; color: #ff5050; font-size: 34rpx; text-align: right;height: 100%; padding-top: 18rpx; box-sizing: border-box;}


</style>
