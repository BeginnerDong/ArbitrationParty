<template>
	<view class="attPro-container">
		<view class="attPro-tit">
			{{mainData.title}}
		</view>
		<view  class="content ql-editor" style="width: 100%;">
			<view v-html="mainData.content">
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
				mainData:{
					title:'',
					content:''
				},
				thirdInfo:{
					name:'',
					account:''
				},
				messageData:[],
				paginate:{},
				title:''
			}
		},

		onLoad(options) {
			const self = this;
			self.title = options.title;
			self.$Utils.loadAll(['getMainData'], self);
			
		},
		
		onShow() {
			const self = this;
			
		},
		



		methods: {
			
			
			getMainData() {
				const self = this;
				const postData = {
					searchItem:{
						title:self.title
					}	
				};
				const callback = (res)=>{
					if(res.solely_code==100000){
						if(res.info.data.length>0){
							self.mainData = res.info.data[0];
						}else{
							uni.showToast({
								title: '没有文章',
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
				self.$apis.articleGet(postData, callback);
				
			},
			
						
		},
	
	}
</script>

<style>
	.attPro-tit{
		height: 100rpx;
		line-height: 100rpx;
		padding-top: 20rpx;
		text-align: center;
	}
	 .attPro-container .ql-editor{
		 padding: 20rpx;
		font-size: 28rpx;
		line-height: 44rpx;
	}
	/*
	* .attPro-container .ql-editor uni-view{
		width: 100%;
	}
	.attPro-container .ql-editor uni-view>p{
		width: 100%;
	}
	.attPro-container img{
		width: 100%;
	}*/
	@import "../../assets/style/proDetails.css";
	@import "../../assets/style/quill.css";
</style>
