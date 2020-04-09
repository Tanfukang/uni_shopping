<template>
	<view class="box">
		<!-- 搜索栏 -->
		<view class="search-box">
			<view class=" com-box" @click="toindex">
				<image src="../../static/xie/arrow-left.png" class="bgimg"></image>
			</view>
			<view class=" inp-box">
				<view>
					<image src="../../static/xie/搜索%20(1).png" class="serchimg"></image>
				</view>
				<view class="inp"><input type="text" :placeholder="search" v-model="searchtet" /></view>
			</view>
			<view class=" scan-box" @click="tosacn">搜索</image>
			</view>
		</view>
		<!-- 热搜部分 -->
		<view class="hot-box" v-show="hotbox">
			<!-- 热门搜索 -->
			<view class="tit">热门搜索</view>
			<view style="display: flex;flex-wrap: wrap;">
				<block v-for="item in handpick">
					<view class="handpick-num">{{item}}</view>
				</block>
			</view>
			<!-- 常用分类 -->
			<view class="tit">常用分类</view>
			<view style="display: flex;flex-wrap: wrap;">
				<block v-for="item in clanum">
					<view class="clatet">{{item}}</view>
				</block>
			</view>
			<view style="background: #F5F5F5;height:20upx;margin: 30upx 0;"></view>
			<!-- 搜索历史 -->
			<view class="hist-list">
				<view class="tit">搜索历史</view>
				<block v-for="item in histlist">
					<view class="histnam">{{item}}</view>
				</block>
			</view>
		</view>
		<searchcommodity :paren="cooks" :nocomm="nocomm" v-if="commbox" ref="searchcommodity"></searchcommodity>
	</view>
</template>

<script>
	import searchcommodity from '../comm/searchcommodity.vue'
	export default {
		data() {
			return {
				hotbox: true,
				commbox: false,
				search: "智能积木 越野四驱车",
				handpick: ["领劵中心", "Redmi K20", "RedmiBook 14", "智能积木 越野四驱车", "手环 手腕"],
				clanum: ["耳机", "手机", "电脑", "笔记本", "手表", "配件", "保健", "酷玩", "传感器/网关"],
				histlist: ["小米手机", "华为手机"],
				searchtet: "",
				cooks: [],
				nocomm: false
			}
		},
		onLoad() {

		},
		components: {
			searchcommodity
		},
		methods: {
			
			toindex() {
				uni.switchTab({
					url: "../index/index"
				})
			},
			
			tosacn() {
				cooks: [],
				this.hotbox = false,	//热搜栏隐藏
					this.commbox = true,	//搜索结果显示
					uni.request({
						url: "http://ceshi3.dishait.cn/api/goods/search",
						method: "POST",
						data: {
							title: this.searchtet,
							page: 1
						},
						success: (res) => {
							console.log(res.data.data)
							this.cooks = res.data.data
							if (this.cooks == ''||this.cooks==undefined) {	//搜索结果为空时
								this.nocomm = true
								console.log("22222")
							} else {
								this.nocomm = false		//搜索结果不为空时
								console.log("1111")
							}
						}
					})
				
			}
		}
	}
</script>

<style scoped>
	.box {
		width: 100%;
		margin: auto;
	}

	.bor {
		border: #000000 1upx solid;
	}

	.search-box {
		width: 95%;
		height: 80upx;
		margin: 20upx auto;
		display: flex;
		justify-content: space-around;
		border-radius: 15upx;
	}

	.com-box {
		width: 10%;
		height: 100%;
	}

	.inp-box {
		width: 70%;
		height: 80%;
		line-height: 60upx;
		display: flex;
		background: #F0F0F0;
		margin-top: 10upx;
	}

	.inp {
		height: 60upx;
		margin-top: 10upx;
	}

	.scan-box {
		width: 13%;
		height: 100%;
		line-height: 80upx;
		display: flex;
	}

	.bgimg {
		width: 60upx;
		height: 60upx;
		margin-top: 10upx;
	}

	.serchimg {
		width: 40upx;
		height: 40upx;
		margin: 10upx 10upx 20upx 20upx;
	}

	.tet {
		font-size: 28upx;
		color: #7A7E83
	}

	/* 热门搜索 */
	.hot-box {
		width: 99%;
		margin: 30upx auto;
	}

	.tit {
		font-weight: 600;
		margin: 30upx 20upx;
	}

	.handpick-num {
		padding: 5upx 12upx;
		font-size: 28upx;
		margin: 10upx;
	}

	.handpick-num:nth-child(2n) {
		background: #F8EAE9;
		border: 1upx solid #F76260;
	}

	.handpick-num:nth-child(2n-1) {
		background: #F2F6E8;
		border: 1upx solid #4CD964;
	}

	/* 常用分类 */
	.clatet {
		padding: 10upx 15upx;
		font-size: 30upx;
		margin: 10upx;
		background: #F5F5F5;
		color: #C8C7CC;
	}

	/* 搜索历史 */
	.hist-list {
		width: 100%;
		margin: auto;
	}

	.histnam {
		height: 60upx;
		line-height: 60upx;
		font-size: 30upx;
		text-indent: 1rem;
	}
</style>
