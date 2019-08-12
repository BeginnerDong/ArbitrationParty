<template>
	<view class="attPro-container">
		<view class="banner-container">
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
	@import "../../assets/style/proDetails.css";
	@import "../../assets/style/quill.css";
</style>
