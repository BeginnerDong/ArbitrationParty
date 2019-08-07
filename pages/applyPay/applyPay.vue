<template>
	<view class="container">
		<view class="name-container">
			<view class="title">申请金额：</view>
			<input @input="changePrice" v-model="submitData.price" type="text" placeholder="请输入申请金额" placeholder-style="color:#999999;font-size:12px;" />
		</view>
		
		<view class="name-container">
			<view class="title">手续费：</view>
			{{submitData.fee}}
		</view>
		
		<view class="name-container">
			<view class="title">手续费承担方：</view>
			<view class="style-container">
			 <view class="style-little-container" @click="submitData.pay_type=1">
				<image src="../../static/images/form-icon1.png"/>
				<text :style="submitData.pay_type==1?'color:red':''" >甲方</text>
			 </view>
			<view class="style-little-container" @click="submitData.pay_type=2">
				<image src="../../static/images/form-icon1.png"/>
				<text :style="submitData.pay_type==2?'color:red':''" > 乙方</text>
			</view>
			<view class="style-little-container" @click="submitData.pay_type=3">
				<image src="../../static/images/form-icon1.png"/>
				<text :style="submitData.pay_type==3?'color:red':''" >双方平摊</text>
			</view>
		</view>
		</view>
		
		<view class="tip-container">
			<view class="title">申请理由:</view>
			<textarea v-model="submitData.content" type="text" placeholder="请输入您的申请理由" placeholder-style="color:#999999;font-size:11px;" />
		</view>
		<view class="tip-container">
			<view class="title">验收附件：</view>
			<view><p>上传点击无效请点击右上角复制链接，用其他手机浏览器打开</p></view>
			<view class="right-uppic">
				<image @click="upload" class="icon" src="../../static/images/form-icon3.png"/>
			</view>
			<view >
				<template v-for="item in submitData.mainImg" >
					<image :key="item.id" v-if="item.type=='image'" :src="item.url"></image>
					<view :key="item.id" v-else >{{item.name}}</view>
				</template>
			</view>
		</view>

		<view class="submit" @click="webSelf.$Utils.stopMultiClick(submit)"><button>确认</button></view>
		<cUpload @uploadAfter="uploadAfter" ref="cUpload" ></cUpload>
	
	</view>
</template>

<script>
	import cUpload from "@/components/upload/upload.vue"
	export default {
		components: {
			cUpload
		},
		data() {
			return {
				webSelf: this,
				isShow:false,
				project_no:'',
				submitData:{
					fee:'',
					pay_type:'',
					content:'',
					price:0,
					mainImg:[],
					type:3
				}
			}
		},
	
		onLoad(options) {
			const self = this;
			self.project_no = options.project_no;
			self.submitData.project_no = self.project_no;
			self.submitData.role = options.role;
		},
		
		onShow() {
			const self = this;
			document.title = '申请付款'			
		},
		methods: {
			
			changePrice(){
				const self = this;
				if(self.submitData.price){
					var ratio = parseFloat(uni.getStorageSync('user_info').thirdApp.ratio).toFixed(2);
					self.submitData.fee = (self.submitData.price*ratio/100).toFixed(2);
				};
				
			},
			
			submit(){
				const self = this;
				const postData = {
					tokenFuncName:'getProjectToken',
					data:self.submitData
				};
				const callback = (res)=>{
					if(res.solely_code==100000){
						uni.showToast({
							title: '提交成功',
							duration: 1000,
							complete:function(){
								uni.setStorageSync('canClick', true);
								setTimeout(function(){
									uni.navigateBack({
										delta: 1
									});
								},1000);	
							}
						});
					}else{
						uni.showToast({
							title: '提交失败',
							duration: 1000,
							complete:function(){
								uni.setStorageSync('canClick', true);
							}
						});
					}
				};
				self.$apis.processAdd(postData, callback);
			},
			upload(){
				const self = this;
				self.$refs.cUpload.customButtonClick();
			},
			uploadAfter(res){
				const self = this;
				self.submitData.mainImg.push(res);
			},
		
			
		
		}
	}
	
</script>

<style>
	@import "../../assets/style/applyPay.css";
	.right-uppic{width: 20%; height: 90px; padding: 4%; background-color: rgb(243,243,243); position: relative;}  
	.right-uppic input{ width: 100%; height: 100%; opacity: 0.5;}
	.right-uppic .icon{width:64rpx;height: 64rpx;position: absolute;left: 50%;top: 50%;transform: translate(-50%,-50%);}
	
</style>
