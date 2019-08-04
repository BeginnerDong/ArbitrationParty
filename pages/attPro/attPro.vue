<template>
<view class="attPro-container">
   <view class="banner-container" :class="{fixTitle:whether}">
        <view @click="num=0" :class="{'active-item':num===0}"  class="item"><view class="text">进行中</view></view>
        <view @click="num=1" :class="{'active-item':num===1}"  class="item"><view class="text">已完结</view></view>
    </view>
<view class="tab-con">
	<view v-show="num===0">
        <view class="tip-big-container">
			<!-- first -->
			<view class="tip-container"   @click="webSelf.$Router.navigateTo({route:{path:'/pages/proDetails/proDetails'}})">
				<view class="tip">
					<image src="../../static/images/canyu-icon3.png"/>
					<view class="title">产品名称：</view>
					<view class="name">名称名称名称名称</view>
				</view>
				
				<view class="tip">
					<image src="../../static/images/canyu-icon4.png"/>
					<view class="title">交易类型：</view>
					<view class="name">cpa</view>
					<view class="arrow"></view>
				</view>
				
				<view class="tip">
					<image src="../../static/images/canyu-icon5.png"/>
					<view class="title">我的角色：</view>
					<view class="name">甲方</view>
				</view>
				<view>
					<image class="fxdIcon" src="../../static/images/canyu-icon2.png" mode=""></image>
				</view>
				<view class="finishBtn">
					<button type="button">完结</button>
				</view>
			</view>
			<!-- first -->
			
			<!-- first -->
			<view class="tip-container"   @click="webSelf.$Router.navigateTo({route:{path:'/pages/proPartake/proPartake'}})">
				<view class="tip">
					<image src="../../static/images/canyu-icon3.png"/>
					<view class="title">产品名称：</view>
					<view class="name">名称名称名称名称</view>
				</view>
				
				<view class="tip">
					<image src="../../static/images/canyu-icon4.png"/>
					<view class="title">交易类型：</view>
					<view class="name">cpa</view>
					<view class="arrow"></view>
				</view>
				
				<view class="tip">
					<image src="../../static/images/canyu-icon5.png"/>
					<view class="title">我的角色：</view>
					<view class="name">乙方</view>
				</view>
				<view>
					<image class="fxdIcon" src="../../static/images/canyu-icon1.png" mode=""></image>
				</view>
			</view>
			<!-- first -->
			
			<!-- first -->
			<view class="tip-container"  @click="webSelf.$Router.navigateTo({route:{path:'/pages/proPartake/proPartake'}})">
				<view class="tip">
					<image src="../../static/images/canyu-icon3.png"/>
					<view class="title">产品名称：</view>
					<view class="name">名称名称名称名称</view>
				</view>
				
				<view class="tip">
					<image src="../../static/images/canyu-icon4.png"/>
					<view class="title">交易类型：</view>
					<view class="name">cpa</view>
					<view class="arrow"></view>
				</view>
				
				<view class="tip">
					<image src="../../static/images/canyu-icon5.png"/>
					<view class="title">我的角色：</view>
					<view class="name">甲方</view>
				</view>
				<view>
					<image class="fxdIcon" src="../../static/images/canyu-icon1.png" mode=""></image>
				</view>
			</view>
			<!-- first -->
		</view>
    </view>
	<view v-show="num===1">
        <view class="tip-big-container">
       	<!-- first -->
       	<view class="tip-container"  @click="webSelf.$Router.navigateTo({route:{path:'/pages/proDetailFinish/proDetailFinish'}})">
       		<view class="tip">
       			<image src="../../static/images/canyu-icon3.png"/>
       			<view class="title">产品名称：</view>
       			<view class="name">名称名称名称名称</view>
       		</view>
       		
       		<view class="tip">
       			<image src="../../static/images/canyu-icon4.png"/>
       			<view class="title">交易类型：</view>
       			<view class="name">cpa</view>
				<view class="arrow"></view>
       		</view>
       		
       		<view class="tip">
       			<image src="../../static/images/canyu-icon5.png"/>
       			<view class="title">我的角色：</view>
       			<view class="name">甲方</view>
       		</view>
			<view>
				<image class="fxdIcon" src="../../static/images/canyu-icon2.png" mode=""></image>
			</view>
       	</view>
       	<!-- first -->
       	
       	<!-- first -->
       	<view class="tip-container"   @click="webSelf.$Router.navigateTo({route:{path:'/pages/proDetailFinish/proDetailFinish'}})">
       		<view class="tip">
       			<image src="../../static/images/canyu-icon3.png"/>
       			<view class="title">产品名称：</view>
       			<view class="name">名称名称名称名称</view>
       		</view>
       		
       		<view class="tip">
       			<image src="../../static/images/canyu-icon4.png"/>
       			<view class="title">交易类型：</view>
       			<view class="name">cpa</view>
				<view class="arrow"></view>
       		</view>
       		
       		<view class="tip">
       			<image src="../../static/images/canyu-icon5.png"/>
       			<view class="title">我的角色：</view>
       			<view class="name">乙方</view>
       		</view>
			<view>
				<image class="fxdIcon" src="../../static/images/canyu-icon1.png" mode=""></image>
			</view>
       	</view>
       	<!-- first -->
       	
       	<!-- first -->
       	<view class="tip-container"   @click="webSelf.$Router.navigateTo({route:{path:'/pages/proDetailFinish/proDetailFinish'}})">
       		<view class="tip">
       			<image src="../../static/images/canyu-icon3.png"/>
       			<view class="title">产品名称：</view>
       			<view class="name">名称名称名称名称</view>
       		</view>
       		
       		<view class="tip">
       			<image src="../../static/images/canyu-icon4.png"/>
       			<view class="title">交易类型：</view>
       			<view class="name">cpa</view>
				<view class="arrow"></view>
       		</view>
       		
       		<view class="tip">
       			<image src="../../static/images/canyu-icon5.png"/>
       			<view class="title">我的角色：</view>
       			<view class="name">甲方</view>
       		</view>
			<view>
				<image class="fxdIcon" src="../../static/images/canyu-icon1.png" mode=""></image>
			</view>
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
			const self = this;
			
		},
		
		onShow() {
			const self = this;
			document.title = '参与项目'			
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
	@import "../../assets/style/attPro.css";
	.finishBtn {overflow: hidden;}
	.finishBtn button{ width:120rpx; height:50rpx; text-align: center; line-height:50rpx; color: #00A1E9; border-radius: 8rpx; border: 1px solid #00A1E9; font-size: 26rpx; float: right; margin-right: 20rpx;}
</style>
