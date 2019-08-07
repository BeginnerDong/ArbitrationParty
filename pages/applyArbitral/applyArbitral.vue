<template>
	<view class="arbitral-big-container">
		
		<view class="arbitral-container">
			<view class="arbitral-img-text" @click="arbitration_type=1">
				<image src="../../static/images/apply-icon2.png"/>
				<view :style="arbitration_type==1?'color:red':''">平台仲裁</view>
			</view>
			<view class="arbitral-img-text" @click="arbitration_type=2">
				<image src="../../static/images/apply-icon4.png"/>
				<view :style="arbitration_type==2?'color:red':''">全民仲裁</view>
			</view>
		</view>
		
		<view class="button" @click="webSelf.$Router.navigateTo({route:{path:'/pages/applyArbUpPic/applyArbUpPic?project_no='+project_no+'&arbitration_type='+arbitration_type}})"><button>下一步</button></view>
    </view>
</template>

<script>
	export default {
		data() {
			return {
				webSelf: this,
				isShow:false,
				arbitration_type:1,
				project_no:''
			}
		},
	
		onLoad(options) {
			const self = this;
			self.project_no = options.project_no;
		},
		
		onShow() {
			const self = this;
			document.title = '申请仲裁'			
		},
		methods: {
		
				show() {
					const self = this;
					
					self.isShow = !self.isShow
				}
	
	

			}
		}
	
</script>

<style>
	@import "../../assets/style/applyArbitral.css";
</style>
