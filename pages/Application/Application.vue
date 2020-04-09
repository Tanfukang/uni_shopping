<template>
	<view class="container">
		<view class="information">
			<view class="order">订单号：5180925177903542</view>
			<view class="time">下单时间:2018年09月25日 11:34</view>
		</view>
		<view class="merchandise" v-for="(item,index) in png" :key="index">
			<view class="sign">
				<image :src="item.cover"></image>
				<view class="box">
					<view class="name"> {{item.title}}</view>
					<view class="odd">SN：15494***5772</view>
				</view>
				<image src="../../static/jinru.png" class="img"></image>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				png: "" //图片
			}
		},
		methods: {
			getHomeSlideFunc() {
				var _this = this;
				uni.request({
					url: 'http://ceshi3.dishait.cn/api/goods/hotlist', //请求接口
					header: {
						'content-type': 'application/x-www-form-urlencoded', //自定义请求头信息
					},
					success: (res) => { //请求成功后返回
						// console.log(res)
						_this.png = res.data.data
						// console.log(_this.png)
					}
				});
			}
		},
		onLoad: function(option) {
			this.getHomeSlideFunc()
		}
	}
</script>

<style>
	.container {
		width: 100%;
		background: #EEEEEE;
	}

	/* 导航栏 */
	.nav {
		width: 100%;
		height: 80upx;
		border-bottom: 5upx solid #F4F4F4;
		line-height: 80upx;
		background: #FAFAFA;
		padding-left: 20upx;
	}

	.nav text {
		display: inline-block;
		padding-left: 20upx;
	}

	/* 订单号及 下单时间 */
	.information {
		width: 100%;
		height: 120upx;
		background: white;
		padding-left: 20upx;
		margin-bottom: 20upx;
	}

	.information .order {
		font-size: 30upx;
		color: #BABABA;
		padding-top: 20upx;
	}

	.information .time {
		font-size: 30upx;
		padding-top: 10upx;
	}

	/* 已购商品 */
	.merchandise {
		width: 100%;
		height: 180upx;
		background: white;
	}

	.merchandise .sign {
		width: 100%;
		height: 180upx;
		border-bottom: #F7F7F7 solid 10upx;
		margin: 10upx 0upx;
	}

	.merchandise .sign image {
		width: 160upx;
		height: 160upx;
		margin-top: 20upx;
		float: left;
	}

	.merchandise .sign .odd {
		font-size: 30upx;
		color: #AAAAAA;
	}

	.merchandise .sign .name {
		font-size: 32upx;
	}
	.merchandise .sign .box{float: left;margin-top: 60upx;line-height: 40upx;margin-left: 20upx;}
	.merchandise .sign .img{width: 40upx;height: 40upx;float: right;margin-top: 65upx;margin-right: 20upx;}
</style>
