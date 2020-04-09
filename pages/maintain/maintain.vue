<template>
	<view class="container">
		<view class="product">
			<view class="title">申请售后的产品</view>
			<view class="youth">
				<image :src="information.cover"></image>
			</view>
			<view class="maintenance">
				<view class="uname">{{information.title}}</view>
				<view class="Aftersale">{{Aftersale}}</view>
			</view>
		</view>
		<view class="servicebox">
			<view class="typeofservice">服务类型</view>
			<view class="service">维修</view>
		</view>
		<view class="problembox">
			<view class="problem">问题描述</view>
			<view class="multiline">
				<textarea maxlength="200" @input="textbox" placeholder="详细描述一下你遇到的问题吧" />
				<view class="quantity">
					<image src="../../static/camera.png"></image>
					<view>{{amount}}/200</view>
				</view>
			</view>
		</view>
		<navigator url="../Application/Application"><button class="btn">下一步</button></navigator>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				information: "",
				Aftersale: "维修服务：剩余111天",
				amount:0
			}
		},
		methods: {
			textbox(e){
				this.amount = e.detail.value.length
				// console.log(e.detail.value.length)
			},
		},
		onLoad: function(option) { //数据接收
			this.information = JSON.parse(decodeURIComponent(option.item))
			// console.log(this.information.cover)
		}
	}
</script>

<style>
	.container {
		width: 100%;
		height: 1200upx;
		background: #EEEEEE;
	}

	/* 申请售后的产品 */
	.product {
		width: 100%;
		height: 220upx;
		padding-left: 40upx;
		background: white;
	}

	.product .youth {
		width: 15%;
		float: left;
	}

	.product .youth image {
		width: 120upx;
		height: 120upx;
		margin-top: 10upx;
	}

	.product .title {
		height: 70upx;
		font-size: 27upx;
		line-height: 70upx;
		border-bottom: 1upx solid #F6F6F6;
		color: #999999;
	}

	.product .maintenance {
		float: left;
		width: 80%;
		height: 120upx;
		margin-left: 30upx;
	}

	.product .maintenance .Aftersale {
		font-size: 27upx;
		color: #999999;
		margin-top: 10upx;
	}

	.product .maintenance .uname {
		margin-top: 30upx;
	}

	/* 维修服务 */
	.servicebox {
		width: 100%;
		height: 220upx;
		background: white;
		margin-top: 20upx;
		padding-left: 40upx;
	}

	.servicebox .typeofservice {
		font-size: 27upx;
		color: #999999;
		height: 60upx;
		border-bottom: 1px solid #F4F4F4;
		width: 100%;
		line-height: 60upx;
	}

	.servicebox .service {
		border: 1px solid #FF6400;
		color: #FF6400;
		font-size: 27upx;
		width: 130upx;
		height: 60upx;
		text-align: center;
		line-height: 60upx;
		margin-top: 40upx;
	}
	/* 问题描述 */
	.problembox{width:100%;height:420upx;margin-top:20upx;background:white;padding-left: 40upx;}
	.problembox .problem{font-size:27upx;width:100%;height:60upx;line-height:60upx;border-bottom:1upx solid #F4F4F4;color:#999999;}
	.problembox textarea{border:1upx solid #EBEBEB;width:88%;margin-top:30upx;padding-left:20upx;padding-top:20upx;}
	.problembox image{width:60upx;height:60upx;float: left;padding-left: 20upx;}
	.problembox .quantity view{color:#D8D8D8;font-size:27upx;float: right;}
	
	.multiline{position:relative;}
	.problembox .quantity{position: absolute;bottom: 0upx;width:88%;line-height: 60upx;}
	
	.btn{width:90%;background:#FF6B01;color:white;margin-top:30upx;}
</style>
