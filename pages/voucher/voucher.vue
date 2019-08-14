<template>
	<view class="container">
		<view class="tip-container  formLis">
			<view class="title">申请理由</view>
			<view class="rightBox">
				<textarea v-model="submitData.content" type="text" placeholder="请输入您的申请理由" placeholder-style="color:#999999;font-size:11px;" />
			</view>
		</view>
		<view class="img-container formLis">
			<view class="title">验收附件</view>
			<view class="rightBox">
				<view class="text-container">
					<view><p>可上传图片或者文件</p></view>
					<view><p>上传点击无效请点击右上角复制链接，用其他手机浏览器打开</p></view>
					<view><p class="p2">(可上传多张)</p></view>
				</view>
				<view>
					<image class="uploadBtn" @click="upload" src="../../static/images/form-icon3.png"/>
				</view>
				<view  class="addImgbox">
					<template v-for="item in submitData.mainImg" >
						<image :key="item.id" v-if="item.type=='image'" :src="item.url"></image>
						<view class="fileBox" :key="item.id" v-else >{{item.name}}</view>
					</template>
				</view>
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
					content:'',
					mainImg:[],
					type:4
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
			document.title = '提交表单'			
		},
		methods: {
			
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
								
								setTimeout(function(){
									uni.navigateBack({
										delta: 1
									});
								},1000);	
							}
						});
					}else{
						uni.showToast({
							title: res.msg,
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
	/* @import "../../assets/style/form.css"; */
	@import "../../assets/style/common.css";
	@import "../../assets/style/addDynamic.css";
</style>
