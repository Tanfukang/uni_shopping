<template>
	<view class="container">
		<view class="top">
			<view class="title" v-for="(item,index) in title" :key="index" @click="show(index)">
				<view :class="[vid == index?'hover':'icon-bukejian']">{{item.uname}}</view>
			</view>
		</view>
		<view class="middle">
			<view class="title">设备号申请</view>
			<view><input type="text" placeholder="请输入lMEl或SN码   获取本机lMEl" /><button>申请售后</button></view>
		</view>
		<view class="bottom">
			<view class="title">{{time}}</view>
			<view v-for="(item,index) in information" :key="index" class="list" @click="center(item)">
				<image :src="item.cover"></image>
				<view class="uname">
					<view class="designation">{{item.title}}</view>
					<view class="numbers">lMEl:8698090****0476</view>
				</view>
				<button>申请售后</button>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				information: "",
				time: "2018-09-25 11:34",
				title: [{
						uname: "售后申请",
						"index": "0"
					},
					{
						uname: "进度查询",
						"index": "1"
					},
				],
				vid:0
			}
		},
		methods: {
			center(info){
				// console.log(info)
				uni.navigateTo({
				    url: "../maintain/maintain?item="+encodeURIComponent(JSON.stringify(info))+"" //数据传参
				});
			},
			add() {
				var _this = this;
				uni.request({
					url: 'http://ceshi3.dishait.cn/api/goods/hotlist', //请求接口
					header: {
						'content-type': 'application/x-www-form-urlencoded', //自定义请求头信息
					},
					success: (res) => { //请求成功后返回
						// console.log(res)
						_this.information = res.data.data

					}
				});
			},
			show(index){
				// console.log(index)获取下标
				 this.vid = index //下标赋值
			}
		},
		onLoad: function(option) {
			this.add()
		}
	}
</script>

<style>
	.container {
		width: 100%;
		height: 1600upx;
		background: #EEEEEE;

	}

	/* tab切换售后和进度 */
	.top {
		width: 100%;
		height: 100upx;
		background: white;
		line-height: 100upx;
	}

	.top .title {
		float: left;
		width: 48%;
		text-align: center;
	}

	/* 设备号申请 */
	.middle {
		width: 100%;
		height: 220upx;
		background: white;
		margin-top: 20upx;
		padding-left: 20upx;
	}

	.middle .title {
		font-size: 27upx;
		width: 100%;
		height: 80upx;
		border-bottom: 1upx solid #EEEEEE;
		line-height: 80upx;
	}

	.middle input {
		border-bottom: 1upx solid #999999;
		width: 65%;
		height: 60upx;
		float: left;
		margin-top: 40upx;
		font-size: 28upx;
	}

	.middle button {
		width: 25%;
		height: 70upx;
		color: #FF7B1D;
		border: 1upx solid #FF7B1D;
		font-size: 28upx;
		float: left;
		margin-left: 20upx;
		margin-top: 40upx;
	}

	/* 商品 */
	.bottom {
		width: 100%;
		padding-left: 20upx;
		background: white;
		margin-top: 20upx;
	}

	.bottom .title {
		width: 100%;
		height: 80upx;
		border-bottom: 1upx solid #EEEEEE;
		font-size: 28upx;
		line-height: 80upx;
		color: #C7C7C7;
	}

	.bottom view image {
		width: 140upx;
		height: 140upx;
		float: left;
	}

	.bottom view .uname {
		float: left;
		width: 360upx;
		height: 140upx;
		line-height: 120upx;
		padding-left: 20upx;
	}

	.bottom view .uname view {
		width: 100%;
		height: 40upx;
	}

	.bottom view .uname .designation {
		font-size: 30upx;
	}

	.bottom view .uname .numbers {
		font-size: 27upx;
		color: #B0B0B0;
	}

	.bottom .list {
		width: 100%;
		height: 160upx;
		padding: 20upx 0upx;
		border-bottom: 1upx solid #F5F5F5;
	}

	.bottom .list button {
		width: 25%;
		height: 70upx;
		color: #FF7B1D;
		border: 1upx solid #FF7B1D;
		font-size: 28upx;
		float: left;
		margin-top: 40upx;

	}

	.hover {
		color: #FE8757;
		border-bottom: 2upx solid #FF682A;
	}
</style>
