<template>
	<view style="height: 100%;">
		<view class="title">
			<view class="title-top">
				购物车
			</view>
			<view class="title-edit" @click="txtClick">
				{{edit}}
			</view>
		</view>
		<scroll-view scroll-y="ture" class="main">
			<view class="cart-empty" v-show="cart==''">
				<image src="../../static/shopping.png" mode=""></image>
				<text>购物车还是空的</text>
				<button>去逛逛</button>
			</view>
			<view class="cart">
				<view class="cart-li" v-for="(item,index) in cart" :key="item.id">
					<view class="group">
						<checkbox-group @change="checkboxChange">
							<label>
								<checkbox  color="#DD524D" @change="selected(checked)"  :checked="item.checked" :value="item.id"  />
							</label>
						</checkbox-group>
					</view>
					<image :src="item.cover" mode=""></image>
					<view style="display: inline-block; width: 400upx;overflow: hidden;height: auto;">
						<view class="cart-li-txt">
							<view>{{item.title}}</view>
							<view>{{item.skusText}}</view>
						</view>
						<view class="cart-li-txt">
							<view class="" style="vertical-align: bottom;">
								<text style="color: #DD524D;margin-right: 50upx;">¥{{item.pprice}}</text>
								<text @click="reduce(item)">[-]</text>
								{{item.num}}
								<text @click="add(item)">[+]</text>
								<!-- <text class="del" @click="del(item,index)">删除</text> -->
							</view>
						</view>
					</view>
				</view>
			</view>
			<view class="recommended">
				<view class="rec-txt">
					<view class="rec-txt-t">为你推荐</view>
					<view class="rec-txt-b">——————————— 买了的人还买了 ———————————</view>
				</view>
				<recommended></recommended>
			</view>
		</scroll-view>
		<view class="footer">
			<view class="footer-item">
				<view class="checkbox-icon">
					<checkbox-group @change="selectedall()">
						<checkbox class="quanxuananniu" :checked="allchecked" />
					</checkbox-group>
				</view>	
			</view>
			<view class="total">合计:
				<text class="money"> ￥ {{money}}</text>
			</view>
			<view class="shop-footer-item">
				<button class="settlement-btn">结算</button>
			</view>
		</view>
	</view>
</template>

<script>
	import recommended from "../../components/recommended.vue";
	export default {
		components: {
			recommended
		},
		data() {
			return {
				edit: "编辑",
				allSelect: false,
				money: 0,
				cart: '',
				flag: true, // 用于判断用户购物车是否有商品，没有商品为true，有商品为false
				allchecked: true //默认全选为true，因为后台数据没有是否选中的信息
			}
		},
		onLoad() {
			// uni.request({
			// 	url: 'http://ceshi3.dishait.cn/api/login',
			// 	method: 'POST',
			// 	data: {
			// 		username: 'user2',
			// 		password: 'zcmcss'
			// 	},
			// 	success: (res) => {
			// 		console.log(res.data.data.token)
			// 	}
			// });
			uni.request({
				url: 'http://ceshi3.dishait.cn/api/cart',
				header: {
					'token': 'eb1b0ea6880bcf429fcf39dafd04c4364f87a692'
				},
				success: (res) => {
					this.cart = res.data.data;
					console.log(this.cart)
				}
			});
		},
		methods: {
			txtClick() {
				console.log('编辑点击了')
			},
			// 单个商品前的勾选
			selected(item) {
				console.log(item)
				item.checked = !item.checked
				if (!item.checked) {
					this.allchecked = false
				} else {
					const test = this.cartlist.every(item => {
						return item.checked === true
					})
					if (test) {
						this.allchecked = true
					} else {
						this.allchecked = false
					}
				}
			},
			selectedall() {
				this.allchecked = !this.allchecked
				if (this.allchecked) {
					this.cartlist.map(item => {
						item.flag = true
					})
				} else {
					this.cartlist.map(item => {
						item.flag = false
					})
				}
			}
		}
	}
</script>

<style scoped>
	.main {
		padding: 100upx 0;
		height: calc(100% - 200upx);
		width: 100%;
		overflow: hidden;
		word-wrap: break-word;
	}

	.cart-li {
		height: 200upx;
		width: 94%;
		margin: 0 auto;
		padding: 20upx 0;
		border-bottom: 4upx #BEBEBE solid;
	}

	.cart {
		position: relative;
		padding-left: 50upx;
	}

	.cart .group {
		/* position: absolute;
		left: 10upx;
		top: 150upx; */
		vertical-align: middle;
		display: inline-block;
	}

	.cart-li>image {
		height: 150upx;
		width: 150upx;
		padding: 20upx;
		border: #cccccc 2upx solid;
		display: inline-block;
		vertical-align: middle;
	}

	.cart-li-txt {
		display: inline-block;
		width: 100%;
	}

	.cart-empty {
		height: 100upx;
		width: 100%;
		text-align: center;
		margin: 40upx 0 20upx 0;
	}

	.cart-empty>text {
		color: #C0C0C0;
		font-size: 28upx;
		margin: 0 20upx;
		line-height: 80upx;
	}

	.cart-empty>button {
		display: inline-block;
		width: 180upx;
		height: 70upx;
		vertical-align: middle;
		background-color: #FFFFFF;
		font-size: 30upx;
		line-height: 70upx;
		font-weight: bold;
	}

	.cart-empty image {
		width: 50upx;
		height: 50upx;
		vertical-align: middle;
	}

	.rec-txt {
		padding-top: 50upx;
		padding-bottom: 20upx;
		text-align: center;
		background-color: #F5F5F5;
	}

	.rec-txt-t {
		color: #FD6801;
		font-weight: bold;
		font-size: 40upx;
	}

	.rec-txt-b {
		font-size: 20upx;
		color: #bebebe;
	}

	uni-page-body {
		height: 100%;
	}

	.title {
		font-weight: bold;
		position: fixed;
		top: 0;
		width: 100%;
		height: 100upx;
		line-height: 100upx;
		background-color: #FFFFFF;
		z-index: 999;
	}

	.title-top {
		text-align: center;
	}

	.title-edit {
		position: absolute;
		right: 20upx;
		top: 0;
	}

	.footer {
		font-weight: bold;
		position: absolute;
		bottom: 0;
		width: 100%;
		height: 100upx;
		line-height: 100upx;
		display: flex;
		border-top: #d5d5d6 2upx solid;
		background-color: #FFFFFF;
		z-index: 999;
	}

	.shop-footer-item {
		width: 40%;
		height: 100%;
		margin-left: auto;
	}

	.money {
		color: #FD6801;
	}

	.checkbox-icon {
		width: 160upx;
		padding-left: 40upx;
	}

	.settlement-btn {
		width: 100%;
		height: 100%;
		background-color: #FD6801;
		color: #FFFFFF;
		border-radius: 0;
	}
</style>
<style>
	page {
		height: 100% !important;
	}
</style>
