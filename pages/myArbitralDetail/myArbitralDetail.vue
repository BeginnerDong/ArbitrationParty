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
	  
	   <!-- 弹窗 -->
	   <view id="modal-bg" v-if="isShow"></view>
	   <view id="modal" v-if="isShow">
	   	<view class="title">平台说明</view>
	   	<image src="../../static/images/form-img1.png" class="code"/>
	   	<image src="../../static/images/about-icon8.png" id="close" @click="show()"/>
	   </view>
	   <!-- 弹窗 -->
	   
	</view>
	<view v-show="num===1">
	   <!--项目动态 -->
	     <view class="dynamic-big-container">
			 
			 <view class="dynamic-container">
				 <view class="date-container">
					 <view class="jia">甲方</view>
					 <view class="date">2019.05.23</view>
				 </view>
				 <view class="content">内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容
				 内容内容内容</view>
				 <image src="../../static/images/dynamic-img.png"/>
			 </view>
			 
			 
			 <view class="dynamic-container">
				 <view class="date-container">
					 <view class="jia" style="color:rgb(38,199,72);">乙方</view>
					 <view class="date">2019.05.23</view>
				 </view>
				 <view class="content">内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容
				 内容内容内容</view>
				 <image src="../../static/images/dynamic-img.png"/>
			 </view>
			 
			 <view class="dynamic-container">
				 <view class="date-container">
					 <view class="jia">甲方</view>
					 <view class="date">2019.05.23</view>
				 </view>
				 <view class="content">内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容
				 内容内容内容</view>
				 <image src="../../static/images/dynamic-img.png"/>
			 </view>
			 
			 <view class="dynamic-container">
				 <view class="date-container">
					 <view class="jia" style="color:rgb(38,199,72);">乙方</view>
					 <view class="date">2019.05.23</view>
				 </view>
				 <view class="content">内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容</view>
				 <image src="../../static/images/dynamic-img.png"/>
			</view>
			 
				<view class="button" @click="webSelf.$Router.navigateTo({route:{path:'/pages/addDynamic/addDynamic'}})"><button>添加动态</button></view>
		 </view>
	   <!--项目动态 -->
	</view>
	<view class="fixedZC" @click="showAlert">支持?</view>
	<view class="fixedAlert"  v-if="showView">
		<view class="maincont">
			<view class="firstline">
				<view class="item">
					<image src="../../static/images/support-icon1.png"></image>
					<view class="name">甲方</view>
				</view>
				<view class="item">
					<image src="../../static/images/support-icon.png"></image>
					<view class="name">乙方</view>
				</view>
			</view>
			<view>
				<button class="zcOkBtn"  type="primary">确定</button>
			</view>
			<image class="colseBtn" @click="coloseAlert" src="../../static/images/about-icon8.png" mode=""></image>
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
				isShow:false,
				showView: false
			}
		},

		onLoad(options) {
	
		},
		
		onShow() {
			const self = this;
			document.title = '项目详情'			
		},


		methods: {
			showAlert(){
				this.showView = true;
			},
			coloseAlert(){
				this.showView = false;
			},
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
	.fixedZC{ width: 90rpx; height: 90rpx; line-height: 90rpx; text-align: center; color: #FFFFFF;border-radius: 50%; background: #00A1E9; position: fixed; right: 10rpx; bottom: 20%; z-index: 66; font-size: 26rpx;}
	.fixedAlert{ position: fixed;top: 0; right: 0; bottom: 0; right: 0;background: rgba(0,0,0,0.5); width: 100%; z-index: 99;}
	.maincont{ position: fixed; top: 50%;left: 50%;transform: translate(-50%,-50%); width: 90%; background: #fff; padding:80rpx 20rpx; box-sizing:border-box; border-radius: 12rpx; z-index: 100; }
	.maincont .firstline{display: flex;justify-content : space-around}
	.maincont .item{ width: 50%;justify-content : space-around; text-align: center;}
	.maincont .item image{ width: 100rpx; height: 100rpx;  margin: 0 auto;}
	.maincont .item .name{height: 60rpx; line-height: 60rpx; font-size: 30rpx;}
	.zcOkBtn{ width: 80%; height: 66rpx; line-height: 66rpx; text-align: center; color: #fff; background: #00A1E9;margin:60rpx auto 0 auto; display: block;}
	.colseBtn{ position: absolute;right: 20rpx; top: 20rpx; width: 40rpx; height: 40rpx; display: block;}
</style>
