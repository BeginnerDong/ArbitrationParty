<template>
	<view class="arbitral-big-container">
		
		<view class="arbitral-container">
			
			<view class="arbitral-img-text">
				<image src="../../static/images/apply-icon2.png"/>
				<view>平台仲裁</view>
			</view>
			
			<view class="arbitral-img-text">
				<image src="../../static/images/apply-icon4.png"/>
				<view>全民仲裁</view>
			</view>
		</view>
		
		<view class="button" @click="webSelf.$Router.navigateTo({route:{path:'/pages/applyArbUpPic/applyArbUpPic'}})"><button>下一步</button></view>
    </view>
</template>

<script>
	export default {
		data() {
			return {
				webSelf: this,
				isShow:false
			}
		},
	
		onLoad(options) {
	
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
