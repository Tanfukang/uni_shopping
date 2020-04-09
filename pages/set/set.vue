<template>
	<view class="set">
		<view class="store">
			账号管理
		</view>
		<view class="user_info">
			<view class="info_text">
				个人资料
			</view>
			<view class="right_next">
				<image src="../../static/tan/right.png" mode="" @click="updinfo"></image>
			</view>
		</view>
		<view class="shouhuo">
			<view class="info_text">
				收货地址
			</view>
			<view class="right_next">
				<image src="../../static/tan/right.png" mode="" @click="add"></image>
			</view>
		</view>
		<view class="store">
			关于
		</view>
		<view v-for="(item,index) in setList" :key="index" class="user_info" @click="shoppingInfo(index)">
			<view class="info_text">
				{{item.text}}
			</view>
			<view class="right_next">
				<image src="../../static/tan/right.png" mode=""></image>
			</view>
		</view>
		<!-- 退出登录 -->
		<view class="log_out" @click="logout">
			退出登陆
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				setList: [{
					text: "关于商城"
				}, {
					text: "意见反馈"
				}, {
					text: "协议规则"
				}, {
					text: "资历证件"
				}, {
					text: "用户协议"
				}, {
					text: "隐私政策"
				}]
			}
		},
		methods: {
			updinfo() {
				uni.navigateTo({
					url: '../AlterInfo/AlterInfo'

				});
			},
			add() {
				uni.navigateTo({
					url: '../addr/addr'

				});
			},
			shoppingInfo(index){
				if(index === 0){
					uni.navigateTo({
						url: '../article/article'
					});
				}
			}
		}
	}
</script>

<style scoped>
	.set {
		width: 100%;
		height: 100%;
		overflow: hidden;
		font-size: 30upx;
		background-color: #EEEEEE;
	}

	.store {
		width: 100%;
		height: 100upx;
		line-height: 100upx;
		text-indent: 20upx;
	}

	.user_info {
		width: 100%;
		height: 100upx;
		line-height: 100upx;
		background-color: #FFFFFF;
		overflow: hidden;
		border-bottom: 1upx solid #CCCCCC;
	}

	.info_text {
		text-indent: 20upx;
		float: left;
	}

	.right_next {
		height: 100%;
		float: right;
		margin-top: 10upx;
		margin-right: 20upx;
	}

	.right_next image {
		width: 40upx;
		height: 40upx;
	}

	.shouhuo {
		width: 100%;
		height: 100upx;
		background-color: #FFFFFF;
		line-height: 100upx;
	}

	.user_info:nth-child(10) {
		border: none;
	}

	/* 退出登录 */
	.log_out {
		width: 90%;
		height: 100upx;
		line-height: 100upx;
		background-color: #FFFFFF;
		margin: 30upx auto;
		text-align: center;
	}
</style>
