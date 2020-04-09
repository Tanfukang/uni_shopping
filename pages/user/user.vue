<template>
	<scroll-view class="user" scroll-y="true">
		<!-- 头部信息 -->
		<view class="title">
			<view class="msg">
				<image src="../../static/tan/message.png"></image>
			</view>
			<view class="user-pic">
				<view class="pic-box" @click="info">
					<image src="../../static/tan/logo.jpg"></image>
				</view>
				<view class="user-name">
					测试昵称
				</view>
				<view class="user-vip">
					<image src="../../static/tan/vip.png"></image>
					<text>会员积分1.99</text>
				</view>
			</view>
		</view>
		<!-- 订单 -->
		<view class="order">
			<view class="my-order">
				我的订单
			</view>
			<view class="all-order">
				全部订单<image src="../../static/tan/you.png"></image>
			</view>
		</view>
		<!-- 选项列表 -->
		<view class="sever">
			<view class="sever-list" v-for="(item,index) in severList" :key="index" @click="after(index)">
				<image :src="item.icon" mode=""></image>
				<text>{{item.text}}</text>
			</view>
		</view>
		<!-- 广告 -->
		<view class="adv">
			<image :src="adv"></image>
		</view>
		<!-- 设置列表 -->
		<view class="set-list">
			<view class="list-box" v-for="(item,idx) in setList" :key="idx">
				<view class="set-pic">
					<image :src="item.pic"></image>
					<text>{{item.text}}</text>
				</view>
				<view class="set-btn">
					<image src="../../static/tan/right.png"></image>
				</view>
			</view>
		</view>
		<!-- 设置 -->
		<view class="set">
			<view class="set-pic">
				<image src="../../static/tan/set.png"></image>
				<text>更多设置</text>
			</view>
			<view class="set-btn">
				<image src="../../static/tan/right.png" @click="set"></image>
			</view>
		</view>
	</scroll-view>
</template>

<script>
	export default {
		data() {
			return {
				adv:"",
				severList: [{
						text: "待付款",
						icon: "../../static/tan/pay.png"
					},
					{
						text: "待收货",
						icon: "../../static/tan/shouhuo.png"
					},
					{
						text: "待评价",
						icon: "../../static/tan/pingjia.png"
					},
					{
						text: "退换修",
						icon: "../../static/tan/weixiu.png"
					}
				],
				setList:[
					{
						pic:"../../static/tan/huiyuan.png",
						text:"小米会员"
					},
					{
						pic:"../../static/tan/vip_user.png",
						text:"会员中心"
					},
					{
						pic:"../../static/tan/sever.png",
						text:"服务中心"
					},
					{
						pic:"../../static/tan/home.png",
						text:"小米之家"
					},
					{
						pic:"../../static/tan/gengduo.png",
						text:"更多功能"
					}
				]
			}
		},
		onLoad(){
			uni.request({
				url:'http://ceshi3.dishait.cn/api/index_category/1/data/1',
				success:(res)=>{
					this.adv = res.data.data[0].data[2].src		// 轮播图
				}
			});
		},
		methods:{
			info(){
				uni.navigateTo({
					url: '../AlterInfo/AlterInfo'
					
				});
			},
			set(){
				uni.navigateTo({
					url: '../set/set'
					
				});
			},
			after(){
				uni.navigateTo({
					url: '../aftersales/aftersales'
					
				});
			}
		}
	}
</script>

<style>
	.user {
		width: 100%;
		height: 100%;
		font-size: 30upx;
		overflow: hidden;
		background-color: #F5F5F5;
	}

	.title {
		width: 100%;
		height: 300upx;
		position: relative;
		background: url(../../static/tan/bg.jpg)0 0 no-repeat;
		background-size: cover;
	}

	.msg {
		width: 100%;
		height: 120upx;
		line-height: 120upx;
		text-align: right;
		display: flex;
		overflow: hidden;
	}

	.msg image {
		width: 50upx;
		height: 50upx;
		margin: auto;
		margin-right: 30upx;
	}

	.user-pic {
		width: 100%;
		height: 120upx;
		position: relative;
	}

	.pic-box {
		width: 120upx;
		height: 120upx;
		margin: 0upx 30upx;
		border: 1px solid #FFFFFF;
		border-radius: 50%;
		background-color: #FFFFFF;
		box-sizing: border-box;
	}

	.user-pic view {
		float: left;
	}

	.pic-box image {
		width: 100%;
		height: 100%;
		border-radius: 50%;
	}

	.user-name {
		width: 200upx;
		height: 100%;
		line-height: 120upx;
		color: #F9E8DC;
		text-align: center;
	}

	.user-vip {
		background-color: #FFD43F;
		width: 300upx;
		height: 60upx;
		line-height: 60upx;
		position: absolute;
		right: 0;
		bottom: 0;
		overflow: hidden;
		border-radius: 30upx 0upx 0upx 30upx;
	}

	.user-vip image {
		display: inline-block;
		width: 40upx;
		height: 40upx;
		margin-bottom: 10upx;
		margin-left: 30upx;
		vertical-align: middle;
	}

	.user-vip text {
		margin-left: 15upx;
		display: inline-block;
		font-size: 25upx;
		color: #E49925;
	}

	.order {
		width: 100%;
		padding: 20upx;
		box-sizing: border-box;
		display: flex;
		justify-content: space-around;
		background-color: #FFFFFF;
		border-bottom: 1px solid #CCCCCC;
	}

	.order view {
		width: 50%;
	}

	.my-order {
		font-weight: 700;
	}

	.all-order {
		text-align: right;
	}

	.all-order image {
		width: 30upx;
		height: 30upx;
		margin-bottom: 5upx;
		margin-left: 10upx;
		vertical-align: middle;
	}
	.sever{
		width: 100%;
		height: 150upx;
		background-color: #FFFFFF;
		display: flex;
		justify-content:space-between;
	}
	.sever-list{
		width: 25%;
		height: 100%;
		text-align: center;
	}
	.sever-list image{
		width: 50upx;
		height: 50upx;
		margin-top: 20upx;
	}
	.sever-list text{
		display: block;
	}
	.adv{
		width: 100%;
		height: 300upx;
	}
	.adv image{
		width: 100%;
		height: 300upx;
	}
	.set-list view:nth-child(5){
		border: none;
	}
	.list-box{
		width: 100%;
		padding: 30upx;
		box-sizing: border-box;
		display: flex;
		justify-content:space-between ;
		background-color: #FFFFFF;
		border-bottom: 1px solid #CCCCCC;
	}
	.list-box view{
		width: 50%;
	}
	.list-box image{
		width: 30upx;
		height: 30upx;
	}
	.set-pic image{
		margin-right: 30upx;
	}
	.set-btn{
		text-align:right;
	}
	.set{
		width: 100%;
		padding: 30upx;
		box-sizing: border-box;
		margin-top: 20upx;
		display: flex;
		justify-content:space-between ;
		background-color: #FFFFFF;
		border-bottom: 1px solid #CCCCCC;
	}
	.set view{
		width: 50%;
	}
	.set image{
		width: 30upx;
		height: 30upx;
	}
</style>
