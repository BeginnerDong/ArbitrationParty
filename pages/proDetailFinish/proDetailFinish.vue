<template>
	<view class="attPro-container" style="padding-bottom:80rpx;">
		<view class="banner-container" :class="{fixTitle:whether}">
			<view @click="num=0" :class="{'active-item':num===0}" class="item">
				<view class="text">详情</view>
			</view>
			<view @click="num=1" :class="{'active-item':num===1}" class="item">
				<view class="text">动态</view>
			</view>
		</view>
		<view class="tab-con">
			<view v-show="num===0">
				<view class="container">
					<view class="name-container">
						<view class="title">产品名称</view>
						<input type="text" disabled="true" placeholder="产品名称产品名称" placeholder-style="color:rgb(34,34,34);font-size:13px;" />
					</view>

					<view class="cate-container">
						<view class="title">交易类型</view>
						<input type="text" disabled="true" placeholder="uv" placeholder-style="color:rgb(34,34,34);font-size:13px;" />
					</view>

					<view class="rolle-container">
						<view class="title">选择我的角色</view>
						<input type="text" disabled="true" placeholder="乙方" placeholder-style="color:rgb(34,34,34);font-size:13px;" />
					</view>

					<view class="phone-big-container">
						<view class="phone-container">
							<view class="title">填写交易对方手机号</view>
							<input type="text" disabled="true" placeholder="18223025225" placeholder-style="color:rgb(34,34,34);font-size:13px;" />
						</view>
						<view class="info-container">
							<view><text>姓名:</text>张瑞</view>
							<view class="score"><text>信用分:</text>100</view>
							<view><text>已完结交易单数:</text>5</view>
						</view>

					</view>

					<view class="sum-container">
						<view class="title">交易金额</view>
						<input type="text" disabled="true" placeholder="56236" placeholder-style="color:red;font-size:13px;" />
					</view>

					<view class="name-container">
						<view class="title">交易内容</view>
						<input type="text" disabled="true" placeholder="不刷量,不分销" placeholder-style="color:#000;font-size:13px;" />
					</view>

					<view class="tip-container">
						<view class="title">增加内容</view>
						<textarea type="text" placeholder="内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容"
						 placeholder-style="color:#999999;font-size:13px;" />
						</view>
	   	
	   	<view class="img-container">
	   	  <view class="title">附件</view>
		  <view class="img-little-container">
	   	    <image src="../../static/images/img.png"/>
		    <image src="../../static/images/img.png"/>
		    <image src="../../static/images/img.png"/>
		    <image src="../../static/images/img.png"/>
		    <image src="../../static/images/img.png"/>
		  </view>
	   	</view>
		
		<view class="flat-info">
			<view class="phone-big-container">

				<view class="phone-container">
					<view class="title" style="color:#000000;font-size:15px;font-weight:bold;">平台信息</view>
				</view>
				<view class="info-container">
					<view>付款账号</view>
					<input type="text" disabled="true" placeholder="123356968963332" placeholder-style="color:#000;font-size:13px;" />
				</view>
			
			</view>
			
			<view class="phone-container" style="border-bottom:1px solid #F1F1F1;">
				<view class="title">姓名</view>
				<input type="text" disabled="true" placeholder="张三" placeholder-style="color:rgb(34,34,34);font-size:13px;" />
			</view>
		</view>

		   
	   </view>
	   </view>
	  
	   
	</view>
	<view v-show="num===1">
	   <!--项目动态 -->
	     <view class="dynamic-big-container">
			 
			<view class="dynamic-container" v-for="(item,index) in dynami" :key="index"> 
				 <view class="date-container">
					 <!-- 乙方名字颜色 style="color:rgb(38,199,72);" -->
					 <view class="jia">{{item.nameA}}</view>
					 <view class="date">{{item.time}}</view>
				 </view>
				 <view class="content">{{item.cont}}</view>
				 <image :src="item.urlPic"/>
			</view>
			<view class="button" @click="webSelf.$Router.navigateTo({route:{path:'/pages/addDynamic/addDynamic'}})"><button>添加动态</button></view>
		 </view>
	   <!--项目动态 -->
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
				dynami:[
					{
						nameA:"甲方",
						time:"2019.07.30",
						cont:"内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容",
						urlPic:"../../static/images/dynamic-img.png"
					},
					{
						nameA:"乙方",
						time:"2019.07.30",
						cont:"内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容",
						urlPic:"../../static/images/dynamic-img.png"
					},
					{
						nameA:"乙方",
						time:"2019.07.30",
						cont:"内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容",
						urlPic:"../../static/images/dynamic-img.png"
					},
					{
						nameA:"乙方",
						time:"2019.07.30",
						cont:"内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容",
						urlPic:"../../static/images/dynamic-img.png"
					}
				]
			}
		},

		onLoad(options) {
	
		},
		
		onShow() {
			const self = this;
			document.title = '项目详情'			
		},


		methods: {

			show() {
				const self = this;
				
				self.isShow = !self.isShow
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
	@import "../../assets/style/proDetails.css";
</style>
