<template>
	<view class="container">
		<view class="nav">
			<view class="topbox">
				<image src="../../static/sousuo.png"></image></i><input type="text" placeholder="智能积木 越野四驱车" />
			</view>
			<view class="message">
				<image src="../../static/xinxi.png" class=""></image>
			</view>
		</view>
		<view class="leftlist">
			<view v-for="(item,index) in classify" :key="index" class="list" @click="list(index)">
				<text :class="[vid == index?'actiov':'icon-bukejian']">{{item}}</text>
			</view>
		</view>
		<view class="rightlist">
			<scroll-view style="height: 1200upx;" :scroll-top="scrollTop" scroll-y="true" @scroll="scroll">
				<view v-for="(item,index) in png" :key='index'>
					<view v-for="(item,index) in item.app_category_items" :key="index" class="introduce">
						<image :src="item.cover"></image>
						<view class="cententSize">分类{{vid}}:商品</view>
					</view>
				</view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				classify: ["分类0", "分类1", "分类2", "分类3", "分类4", "分类5"],//列表数据
				png: '',//图片
				vid: 0,//下标
				scrollTop: 0, //滚动的高度
			}
		},
		methods: {
			//定义获取幻灯片数据的方法getHomeSlide（）
			add() {
				var _self = this;
				uni.request({
					url: 'http://ceshi3.dishait.cn/api/category/app_category', //请求接口
					success: (res) => { //请求成功后返回
						console.log(res)
						// _self.png = res.data.data[0].app_category_items;
						_self.png = res.data.data
						// console.log(res.data.data)
					}
				});
			},
			//传下标
			list(index) {
				var _this = this;
				_this.vid = index
				// console.log(index)
				_this.scrollTop = index * 500
				
			},
			// 列表滚动监听
			scroll: function(e) {
				// console.log(this.vid)
				console.log(e.detail.scrollTop)//滚动数据
				var selt = this
				selt.scrollTop = e.detail.scrollTop
				if(selt.scrollTop >= 0 && selt.scrollTop < 500){
					selt.vid = 0
					console.log(1)//滚动数据
				}else if(selt.scrollTop >= 600 && selt.scrollTop < 900){
					selt.vid = 1
					console.log(2)//滚动数据
				}else if(selt.scrollTop >= 1000 && selt.scrollTop < 1300){
					selt.vid = 2
					console.log(3)//滚动数据
				}else if(selt.scrollTop >= 1400 && selt.scrollTop < 1700){
					selt.vid = 3
					console.log(4)//滚动数据
				}else if(selt.scrollTop >= 1800 && selt.scrollTop < 2100){
					selt.vid = 4
					console.log(5)//滚动数据
				}else if(selt.scrollTop >= 2500 && selt.scrollTop < 3000){
					selt.vid = 5
				}
			}
		},
		onLoad() {
			this.add();
			
		}
	}
</script>

<style scoped>
	.container {
		width: 100%;
	}

	/* 导航栏 */
	.nav {
		width: 95%;
		height: 60upx;
		padding: 20upx 30upx 20upx;
	}

	.nav view input {
		background: #F7F7F7;
		font-size: 30upx;
		width: 100%;
		height: 70upx;
		padding-left: 80upx;
	}

	.nav view image {
		width: 40upx;
		height: 40upx;
		position: absolute;
		top: 15upx;
	}

	.nav .topbox {
		position: relative;
		float: left;
		width: 80%;
		height: 80upx;
	}

	.nav .message {
		width: 60upx;
		height: 70upx;
		float: right;
		margin-top: 15upx;
	}

	.nav .message image {
		width: 60upx;
		height: 60upx;
		margin-top: 14upx;
	}

	/* 分类列表 */
	.leftlist {
		width: 20%;
		border-right: 1px solid #F5F5F5;
		text-align: center;
		float: left;
	}

	.leftlist .list {
		width: 100%;
		height: 100upx;
		text-align: center;
		line-height: 100upx;
		border-bottom: 1px solid #F5F5F5;
	}

	.leftlist .list text {
		font-size: 25upx;
		display: block;
		width: 96%;
		height: 100upx;
		border-left: 10upx solid #FFFFFF;

	}

	/* 纵向可视图滚动组件 */
	.page-section-spacing {
		margin-top: 60rpx;
	}

	.scroll-view_H {
		white-space: nowrap;
	}

	.scroll-view-item {
		height: 300rpx;
	}

	.scroll-view-item_H {
		display: inline-block;
		width: 100%;
		height: 300rpx;
	}

	/* 商品介绍 */
	.rightlist {
		width: 78%;
		float: left;
		text-align: center;
	}

	.rightlist image {
		width: 130upx;
		height: 100upx;
	}

	.rightlist .introduce {
		width: 160upx;
		float: left;
		text-align: center;
		padding: 30upx 15upx;
		text-align: center;
	}

	.cententSize {
		font-size: 25upx;
	}

	/* 点击列表后的样式 */
	.actiov {
		color: #FE6100;
		border-left: 10upx solid #FE6100 !important;
	}
</style>
