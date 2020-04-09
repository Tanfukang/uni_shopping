<template>
	<view class="box">
		<!-- 顶部 -->
		<view class="top">
			<view class="shot">
				<image src="../../static/xie/关闭.png"></image>
			</view>
		</view>
		<view class="title">手机号码登录</view>
		<!-- 输入框 -->
		<view class="from-box">
			<form  @submit="formSubmit" id="from">
			<view class="mar">
				<input type="text" :placeholder="phonenum" class="inp"/>
			</view>
			<view class="verifynum mar">
			<view class="ver1">
					<input type="text" :placeholder="vernum" class="inp"/>
				</view>
				<view class="ver2 col"> 获取验证码</view>
			</view>
			<view class="tet mar"><text  @click="topadpage">用账户密码登录  ></text> </view>
			<view class="mar">
				<button type="primary" :disabled="disabled" form-type="submit">登录</button>
				<checkbox style="transform: scale(0.7);" color="#DD524D" />
				<text class="ps">以阅读并同意小米<text class="blod">账号协议、隐私协议</text>和小米商城 <text class="blod">用户协议</text></text>
			</view>
			</form>
	</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				phonenum:"请输入手机号码",
				vernum:"请输入验证码",
				disabled:false
			}
		},
		methods: {
			formSubmit: function(e) {
				console.log(JSON.stringify(e.detail.value))
			},
			topadpage:function(){
				uni.reLaunch({
					url:"../pad-login/pad-login"
				})
			}
		}
	}
</script>

<style scoped>
	.box {width: 90%;margin: 10upx auto;}
	.col{color:#333333;}
	.bor {border: 1upx solid #4CD964;}
	.tet {line-height: 80upx;font-size: 30upx;color: #2C405A;}
	.top {width: 100%;height: 80upx;display: flex;justify-content: space-between;margin-bottom: 100upx;}

	.shot {width: 80upx;height: 80upx;}

	.shot>image {width: 100%;height: 100%;}

	.title {width: 90%;font-size: 60upx;margin: 50upx auto;}
	
	.from-box {width: 90%;margin: auto;padding: 20upx 0;}
	
	.mar {margin-bottom: 60upx;}
	.inp{width: 100%;line-height: 60upx;height: 60upx;}
	.verifynum{display: flex;justify-content: space-between;}
	.ver1{width: 60%;}
	.ver2{width: 30%;}
	.ps {font-size: 21upx;color: #555555;}
	
	.blod {font-weight: bold;}
</style>
