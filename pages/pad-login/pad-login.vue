<template>
	<view class="box">
		<!-- 顶部 -->
		<view class="top">
			<view class="shot">
				<image src="../../static/xie/关闭.png"></image>
			</view>
			<view class="tet">忘记密码</view>
		</view>
		<view class="title">密码登录</view>
		<view class="from-box">
			<view>
				<input class="urse-input" type="text" v-model="user" :placeholder="ursename" />
			</view>
			<view>
				<input class="psd-input" password type="text" v-model="psd" placeholder="请输入密码"/>
			</view>
			<view class="tet" ><text @click="tophonepage">用手机短信登录 ></text></view>
			<view class="click">
				<button type="primary" :disabled="disabled" @click="touser">登录</button>
				<checkbox style="transform: scale(0.7);" color="#DD524D" :checked="bool" @click="boolfei"/>
				<text class="ps">以阅读并同意小米<text class="blod">账号协议、隐私协议</text>和小米商城 <text class="blod">用户协议</text></text>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				ursename: "请输入手机号/邮箱号/小米账户",
				disabled: true,
				bool:false,
				user:"",
				psd:"",
				msg:""
				
			}
		},
		onLoad() {
			// console.log(this.bool)
		},
		methods: {
			touser(){
				uni.request({
					url:"http://ceshi3.dishait.cn/api/login",
					method:"POST",
					data:{
						username:this.user,
						password:this.psd
					},
					success: (res) => {
						console.log(res)
						this.msg=res.data.msg
						// uni.showToast({
						// 	icon:"none",
						// 	duration:5000,
						// 	title:this.msg
						// })
						if(this.msg=="ok"){
							uni.showToast({
								image:"../../static/xie/正确图标.png",
								title:"正在登陆..."
							})
							setTimeout(()=>{
								uni.reLaunch({
								    url: '../user/user'
								});
							},2000)	
						}else{
							uni.showToast({
								image:"../../static/xie/提示错误图标.png",
								duration:3000,
								title:this.msg
							})
						}
					},
				})
				
			},
			boolfei(){
				this.bool=!this.bool
				console.log(this.bool)
			},
			tophonepage:function(){
				uni.reLaunch({
					url:"../phone-login/phone-login"
				})
			}
		},
		updated() {
			if(this.user!=''&&this.psd!=''&&this.bool!=false){
				this.disabled=false
			}else{
				this.disabled=true
			}
		}
	}
</script>

<style scoped>
	.box {
		width: 90%;
		margin: 10upx auto;
	}

	.bor {
		border: 1upx solid #4CD964;
	}

	.top {
		width: 100%;
		height: 80upx;
		display: flex;
		justify-content: space-between;
		margin-bottom: 100upx;
	}

	.shot {
		width: 80upx;
		height: 80upx;
	}

	.shot>image {
		width: 100%;
		height: 100%;
	}

	.tet {
		line-height: 80upx;
		font-size: 30upx;
		color: #2C405A;
	}

	.title {
		width: 90%;
		font-size: 60upx;
		margin: 50upx auto;
	}

	.from-box {
		width: 90%;
		margin: auto;
		padding: 20upx 0;
	}

	.from-box>view {
		margin-bottom: 60upx;
	}

	.urse-input {
		width: 100%;
		height: 60upx;
		line-height: 60upx;
		border-bottom: 3upx solid #F0AD4E;
	}

	.psd-input {
		width: 100%;
		height: 60upx;
		line-height: 60upx;
		border-bottom: 2upx solid #C8C7CC;
	}

	/* .click>button {
		background:#F0AD4E;
		color: #FFFFFF;
		font-weight: 700;
	} */

	.ps {
		font-size: 21upx;
		color: #555555;
	}

	.blod {
		font-weight: bold;
	}
</style>
