<template>
<view class="attPro-container">
   <view class="banner-container" :class="{fixTitle:whether}">
        <view @click="num=0" :class="{'active-item':num===0}"  class="item"><view class="text">我参与的</view></view>
        <view @click="num=1" :class="{'active-item':num===1}"  class="item"><view class="text">全民仲裁</view></view>
    </view>
<view class="tab-con">
	<view v-show="num===0">
        <view class="tip-big-container">
			<!-- first -->
			<view class="tip-container"   @click="webSelf.$Router.navigateTo({route:{path:'/pages/myArbitralDetail/myArbitralDetail'}})">
				<view class="tip">
					<image src="../../static/images/canyu-icon3.png"/>
					<view class="title">产品名称：</view>
					<view class="name">名称名称名称名称</view>
				</view>
				
				<view class="tip">
					<image src="../../static/images/canyu-icon4.png"/>
					<view class="title">交易类型：</view>
					<view class="name">cpa</view>
				</view>
				
				<view class="tip">
					<image src="../../static/images/canyu-icon5.png"/>
					<view class="title">我的角色：</view>
					<view class="name">甲方</view>
				</view>
				<view class="fixedIcon">全民仲裁</view>
			</view>
			<!-- first -->
			
			<!-- first -->
			<view class="tip-container"   @click="webSelf.$Router.navigateTo({route:{path:'/pages/myArbitralDetail/myArbitralDetail'}})">
				<view class="tip">
					<image src="../../static/images/canyu-icon3.png"/>
					<view class="title">产品名称：</view>
					<view class="name">名称名称名称名称</view>
				</view>
				
				<view class="tip">
					<image src="../../static/images/canyu-icon4.png"/>
					<view class="title">交易类型：</view>
					<view class="name">cpa</view>
				</view>
				
				<view class="tip">
					<image src="../../static/images/canyu-icon5.png"/>
					<view class="title">我的角色：</view>
					<view class="name">乙方</view>
				</view>
				<view class="fixedIcon platform">平台仲裁</view>
			</view>
			<!-- first -->
			
			<!-- first -->
			<view class="tip-container"  @click="webSelf.$Router.navigateTo({route:{path:'/pages/myArbitralDetail/myArbitralDetail'}})">
				<view class="tip">
					<image src="../../static/images/canyu-icon3.png"/>
					<view class="title">产品名称：</view>
					<view class="name">名称名称名称名称</view>
				</view>
				
				<view class="tip">
					<image src="../../static/images/canyu-icon4.png"/>
					<view class="title">交易类型：</view>
					<view class="name">cpa</view>
				</view>
				
				<view class="tip">
					<image src="../../static/images/canyu-icon5.png"/>
					<view class="title">我的角色：</view>
					<view class="name">甲方</view>
				</view>
				<view class="fixedIcon platform">平台仲裁</view>
			</view>
			<!-- first -->
		</view>
    </view>
	<view v-show="num===1">
        <view class="tip-big-container">
       	<!-- first -->
       	<view class="tip-container"  @click="webSelf.$Router.navigateTo({route:{path:'/pages/myArbitralDetail/myArbitralDetail'}})">
       		<view class="tip">
       			<image src="../../static/images/canyu-icon3.png"/>
       			<view class="title">产品名称：</view>
       			<view class="name">名称名称名称名称</view>
       		</view>
       		
       		<view class="tip">
       			<image src="../../static/images/canyu-icon4.png"/>
       			<view class="title">交易类型：</view>
       			<view class="name">cpa</view>
       		</view>
			<view class="fixedIcon">全民仲裁</view>
       		
       	</view>
       	<!-- first -->
       	
       	<!-- first -->
       	<view class="tip-container"   @click="webSelf.$Router.navigateTo({route:{path:'/pages/myArbitralDetail/myArbitralDetail'}})">
       		<view class="tip">
       			<image src="../../static/images/canyu-icon3.png"/>
       			<view class="title">产品名称：</view>
       			<view class="name">名称名称名称名称</view>
       		</view>
       		
       		<view class="tip">
       			<image src="../../static/images/canyu-icon4.png"/>
       			<view class="title">交易类型：</view>
       			<view class="name">cpa</view>
       		</view>
			<view class="fixedIcon">全民仲裁</view>
       		
       	</view>
       	<!-- first -->
       	
       	<!-- first -->
       	<view class="tip-container"   @click="webSelf.$Router.navigateTo({route:{path:'/pages/myArbitralDetail/myArbitralDetail'}})">
       		<view class="tip">
       			<image src="../../static/images/canyu-icon3.png"/>
       			<view class="title">产品名称：</view>
       			<view class="name">名称名称名称名称</view>
       		</view>
       		
       		<view class="tip">
       			<image src="../../static/images/canyu-icon4.png"/>
       			<view class="title">交易类型：</view>
       			<view class="name">cpa</view>
       		</view>
			<view class="fixedIcon">全民仲裁</view>
       	</view>
       	<!-- first -->
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
			document.title = '我的仲裁'			
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
			}						
	},
	handleScroll() {
      var scrollTop =
        window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop;
      // console.log(scrollTop)
      if(scrollTop>329){
        this.whether = true;
      }else{
        this.whether = false;
      }
    }
	}
</script>

<style>
	@import "../../assets/style/myArbitral.css";
</style>
