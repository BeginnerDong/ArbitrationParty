<template>
	<view class="attPro-container">
		<view class="tab-con">
			<view class="tip-big-container"  >
				<view class="tip-container" v-for="item in mainData">
					<view class="tip">
						<view class="title">时间：</view>
						<view class="name">{{item.create_time}}</view>
					</view>
					<view class="tip">
						<view class="title">产品名称：</view>
						<view class="name">{{item.Project.title}}</view>
					</view>
					<view class="tip">
						<view class="title">收款金额：</view>
						<view class="name pub-red">{{item.price}}元</view>
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
				isLoadAll:false
			} 
				
		},

		onLoad(options) {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData'], self);
		},
		
		onShow() {
			const self = this;
			document.title = '交易流水'			
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
			
			getMainData(isNew){
				const self = this;
				if(isNew){
					self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
					self.mainData = [];
				};
				const postData = {
					tokenFuncName:'getProjectToken',
					searchItem:{
						user_no:uni.getStorageSync('user_info').user_no,
						type:5
					},
					paginate:self.$Utils.cloneForm(self.paginate),
					getAfter: {
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
					}
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
					self.$Utils.finishFunc('getProcessData');
				};
				self.$apis.processGet(postData, callback);
			},
					
		}
	}
</script>

<style>
	@import "../../assets/style/myArbitral.css";
	.tip-container{ padding: 0 3%; box-sizing:border-box;}
	.tip-container .tip{ width: 100%; box-sizing:border-box; border-bottom: 2rpx solid #e1e1e1;padding: 0; position: relative; padding-left: 80px;}
	.tip-container .tip:first-child{padding-left: 50px;}
	.tip .title{box-sizing:border-box;width: auto;padding:0;position: absolute; left: 0;}
	.tip .name{ width:100%; overflow: hidden;white-space: nowrap;text-overflow: ellipsis;-o-text-overflow: ellipsis;}
	.tip .name.pub-red{ color: #ff3b3b;}
	.tip .name.pub-blue{ color:#0396ff;}
</style>
