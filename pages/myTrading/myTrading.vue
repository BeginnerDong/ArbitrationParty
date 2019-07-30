<template>
	<view class="attPro-container">
		<view class="tab-con">
			<view class="tip-big-container"  >
				<view class="tip-container">
					<view class="tip">
						<view class="title">时间：</view>
						<view class="name">2019年7月29号</view>
					</view>
					<view class="tip">
						<view class="title">产品名称：</view>
						<view class="name">产品名称内容内容名称内容内容名称内容内容产品名称内容内容名称内容内容名称内容内容产品名称内容内容名称内容内容名称内容内容</view>
					</view>
					<view class="tip">
						<view class="title">收款金额：</view>
						<view class="name pub-red">+2300元</view>
					</view>
				</view>
				<!-- first end -->
				
				<view class="tip-container">
					<view class="tip">
						<view class="title">时间：</view>
						<view class="name">2019年7月29号</view>
					</view>
					<view class="tip">
						<view class="title">产品名称：</view>
						<view class="name">产品名称内容内容名称内容内容名称内容内容产品名称内容内容名称内容内容名称</view>
					</view>
					<view class="tip">
						<view class="title">收款金额：</view>
						<view class="name pub-blue">-2300元</view>
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
                num:0
			} 
				
		},

		onLoad(options) {
	
		},
		
		onShow() {
			const self = this;
			document.title = '交易流水'			
		},


		methods: {
					
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
