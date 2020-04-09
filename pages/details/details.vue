<template>
	<view class="details">
		<view class="title-top">
			<image src="../../static/details/return.png" mode="" @tap="back"></image>
			<image style="float: right;" src="../../static/details/detail.png" mode=""></image>
		</view>
		<view class="details-option-top" :style="{display: display}">
			<image @click="show()" style="float: left;" src="../../static/details/returu2.png" mode=""> </image> 详情页<image style="float: right;"
			 src="../../static/details/detail2.png" mode=""></image>
		</view>
		<image style="width: 100%;" :src="details.cover" mode=""></image>
		<view class="paddinglr">
			<view class="details-title">
				{{details.title}}
			</view>
			<view class="details-desc">
				{{details.desc}}
			</view>
			<view class="details-price"> <text class="details-price-y">￥</text>
				{{details.min_price}} <text class="details-price-y" style="color:rgba(0,0,0,.54) ;"> ￥</text><text class="details-min">
					{{details.min_oprice}}</text></view>
			<scroll-view class="goodsattrs" scroll-x="ture" v-if="details.goodsAttrs!=''">
				<view class="goodsattrs-list" v-for="(item,index) in details.goodsAttrs" :key="index">
					<image src="../../static/details/attrs.png" mode=""></image>
					<view class="goodsattrs-name">{{item.name}}</view>
					<view class="goodsattrs-value">{{item.value}}</view>
				</view>
			</scroll-view>
			<view class="details-option">
				<view @click="showA()">
					<text>已选</text>
					<image class="details-enter" src="../../static/details/enter.png" mode=""></image>
					<view :class="['select','selected',topa]">
						<view style="width: 100%;height:30% ;" @click.native.stop="show()"></view>
						<view class="service-main">

						</view>
						<view class="service-main-bottom" @click.native.stop="show()">加入购物车</view>
					</view>
				</view>
				<view @click="showB()">
					<text style="margin-right: 20upx;">配送   </text>
					<!-- {{address}} -->
					{{address[inx].province}}
					{{address[inx].city}}
					<image class="details-enter" src="../../static/details/enter.png" mode=""></image>
					<view :class="['select','address',topb]">
						<view style="width: 100%;height:30% ;" @click.native.stop="show()"></view>
						<view class="service-main">
							<view class="service-main-top">
								收货地址
							</view>
							<view class="description addresss" v-for="(item,index) in address"  @click.native.stop="shipping(index)">
								<image src="../../static/details/address.png" mode=""></image>
								<view class="address-name">
									{{item.name}} 
								</view>
								<view class="address-city">
									<text>{{item.province}}{{item.city}}{{item.address}}{{item.district}}</text>
								</view>
							</view>
						</view>
						<view class="service-main-bottom" @click.native.stop="">选择新的地址</view>
					</view>
				</view>
				<view class="details-option-hook" @click="showC()">
					<image style="margin-left: 0upx;" src="../../static/details/hook.png" mode=""></image>小米自营
					<image src="../../static/details/hook.png" mode=""></image>小米发货
					<image src="../../static/details/hook.png" mode=""></image>七天无理由退货
					<image class="details-enter" src="../../static/details/enter.png" mode=""></image>
					<view :class="['select','service',topc]">
						<view style="width: 100%;height:30% ;" @click.native.stop="show()"></view>
						<view class="service-main">
							<view class="service-main-top">
								服务说明
							</view>
							<view class="description">
								<image src="../../static/details/hook.png" mode=""></image>
								仿米自营
							</view>
							<view class="description">
								<image src="../../static/details/hook.png" mode=""></image>
								仿米发货
							</view>
							<view class="description-s">
								由仿米发货
							</view>
							<view class="description">
								<image src="../../static/details/hook.png" mode=""></image>
								七天无理由就是不退货
							</view>
							<view class="description">
								<image src="../../static/details/hook.png" mode=""></image>
								运费说明
							</view>
							<view class="description-s">
								不管满多少，就是不包邮；
								特殊产品，也是一样；
							</view>
						</view>
						<view class="service-main-bottom" @click.native.stop="show()">确定</view>
					</view>
				</view>
			</view>
			<scroll-view class="comment" scroll-x="ture" v-if="comment.list!=''">
				<view class="comment-list" v-for="(item,index1) in comment.list" :key="index1">
					<view class="comment-list-tit">
						<image :src="item.user.avatar" mode=""></image>
						<view class="comment-list-tit-mid">
							<text>{{item.user.nickname}}</text>
							<view>
								<text>2019-06-20</text>
							</view>
						</view>
						<view class="comment-list-tit-right">
							<image src="../../static/like.png" mode=""></image>
							<text>{{item.id}}</text>
						</view>
					</view>
					<view class="comment-list-txt">
						{{item.review.data}}
					</view>
					<view class="comment-list-img">
						<image :src="item.review.image" mode=""></image>
					</view>
				</view>
			</scroll-view>
			<view class="more-comment">更多评论<image src="../../static/details/enter.png" mode=""></image>
			</view>
		</view>
		<!-- <view class="content" v-html="details.content"></view> -->
		<view class="content"><img src="http://tangzhe123-com.oss-cn-shenzhen.aliyuncs.com/public/detail_1.png">
			<img src="http://tangzhe123-com.oss-cn-shenzhen.aliyuncs.com/public/detail_2.png">
			<img src="http://tangzhe123-com.oss-cn-shenzhen.aliyuncs.com/public/detail_3.png">
			<img src="http://tangzhe123-com.oss-cn-shenzhen.aliyuncs.com/public/detail_4.png">
			<img src="http://tangzhe123-com.oss-cn-shenzhen.aliyuncs.com/public/detail_5.png">
			<img src="http://tangzhe123-com.oss-cn-shenzhen.aliyuncs.com/public/detail_6.png"></view>
		<view class="recommended-to-you">为您推荐</view>
		<recommended></recommended>
		<view class="bottom"> </view>
		<view class="footer">
			<view class="footer-item">
				<view class="footer-item-favorite">
					<image src="../../static/details/favorite.png" mode=""></image>
					<view>收藏</view>
				</view>
				<view class="footer-item-cart" @click="cart()">
					<image src="../../static/details/cart.png" mode=""></image>
					<view>购物车</view>
				</view>
			</view>
			<view class="shop-footer-item">
				<button class="settlement-btn">加入购物车</button>
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
				details: [],
				comment: [],
				address: [],
				inx:0,
				display: "none",
				topa: "hide",
				topb: "hide",
				topc: "hide"
			}
		},
		onLoad(id) {
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
				url: 'http://ceshi3.dishait.cn/api/useraddresses/1',
				header: {
					'token': 'f74000a8dd9770986e812dcfd1ffb463d3dc0d4b'
				},
				success: (res) => {
					this.address = res.data.data
					console.log(this.address)
				}
			});
			let ids = id.id
			uni.request({
				url: 'http://ceshi3.dishait.cn/api/goods/' + ids,
				success: (res) => {
					this.details = res.data.data;
					console.log('详情', ids, this.details)
				}
			});
			uni.request({
				url: 'http://ceshi3.dishait.cn/api/goods/' + ids + '/comments/good?page=1',
				success: (res) => {
					this.comment = res.data.data
					console.log(ids, this.comment)
				}
			});
			if(this.comment.list==''){
				this.comment.list=this.details.hotComments
			}
		},
		methods: {
			shipping(i){
				this.inx=i
				this.display = "none";
				this.topa = "hide"
				this.topb = "hide"
				this.topc = "hide"
			},
			back() {
				uni.navigateBack(1)
			},
			cart() {
				uni.switchTab({
					url: '/pages/shopping/shopping'
				})
			},
			show() {
				this.display = "none";
				this.topa = "hide"
				this.topb = "hide"
				this.topc = "hide"
			},
			showA() {
				this.display = "block";
				this.topa = "show"
			},
			showB() {
				this.display = "block";
				this.topb = "show"
			},
			showC() {
				this.display = "block";
				this.topc = "show"
			}
		}
	}
</script>

<style scoped>
	.content>>>img {
		width: 100%;
		/* display: block; */
	}

	.content img {
		width: 100%;
	}
	
	.title-top {
		width: 100%;
		height: 100upx;
		position: absolute;
		z-index: 998;
	}

	.title-top image {
		height: 80upx;
		width: 80upx;
		padding: 22upx;
	}

	.details-title {
		font-size: 44upx;
		font-weight: bold;
		margin-top: 20upx;
	}

	.paddinglr {
		padding: 0 20upx;
	}

	.details-desc {
		color: rgba(0, 0, 0, .54);
		font-size: 24upx;
	}

	.details-price {
		color: red;
		margin: 20upx 0;
		font-weight: bold;
	}

	.details-min {
		color: rgba(0, 0, 0, .54);
		font-size: 22upx;
		text-decoration: line-through;
		font-weight: normal;
	}

	.details-price-y {
		font-size: 22upx;
		text-decoration: none;
		position: relative;
		top: -8upx;
	}

	.footer {
		font-weight: bold;
		position: fixed;
		bottom: 0;
		width: 100%;
		height: 100upx;
		display: flex;
		border-top: #d5d5d6 2upx solid;
		background-color: #FFFFFF;
		z-index: 997;
	}

	.footer-item {
		width: 40%;
		height: 100upx;
		text-align: center;
	}

	.footer-item>view {
		width: 50%;
		height: 100%;
		display: inline-block;
		font-size: 22upx;
	}

	.footer-item>view>image {
		margin-top: 5upx;
		width: 45upx;
		height: 45upx;
	}

	.shop-footer-item {
		width: 60%;
		height: 100%;
		margin-left: auto;
	}

	.settlement-btn {
		width: 100%;
		height: 100%;
		font-size: 40upx;
		background-color: #FD6801;
		color: #FFFFFF;
		border-radius: 0;
	}

	.goodsattrs {
		height: 160upx;
		width: 100%;
		white-space: nowrap;
	}

	.goodsattrs-list {
		display: inline-block;
		text-align: center;
		margin-right: 40upx;
		height: 160upx;
	}

	.goodsattrs-list>image {
		width: 50upx;
		height: 50upx;
	}

	.goodsattrs-name {
		font-weight: bold;
	}

	.goodsattrs-value {
		font-size: 20upx;
	}

	.details-option {
		width: 100%;
		border-radius: 15upx;
		background-color: #F5F5F3;
		text-indent: 40upx;
		line-height: 100upx;
		margin: 30upx 0;
	}

	.details-option>view {
		width: 100%;
		height: 100upx;
		border-bottom: 1upx solid #EEEEEC;
	}

	.details-option-hook {
		font-size: 30upx;
	}

	.details-option-hook>image {
		width: 30upx;
		height: 30upx;
		vertical-align: middle;
		margin-left: 20upx;
	}

	.details-enter {
		margin-left: 0upx !important;
		width: 50upx !important;
		height: 50upx !important;
		float: right;
		margin-top: 25upx;
	}

	.select {
		width: 100%;
		height: 100%;
		position: fixed;
		z-index: 998;
		left: 0upx;
		background-color: rgba(0, 0, 0, 0.65);
		transition-duration: 1s
	}

	.hide {
		top: 100%;
	}

	.show {
		top: 0;
	}

	.details-option-top {
		width: 100%;
		height: 100upx;
		position: fixed;
		z-index: 999;
		background-color: #FFFFFF;
		text-align: center;
		font-size: 40upx;
		line-height: 110upx;
	}

	.details-option-top image {
		height: 60upx;
		width: 60upx;
		margin: 22upx;
	}

	.service-main {
		width: 100%;
		height: 80%;
		background-color: #fefeff;
		position: absolute;
		bottom: 0;
		border-radius: 20upx 20upx 0 0;

	}

	.service-main-top {
		width: 90%;
		margin: 0 auto;
		border-bottom: #e6e6e7 2upx solid;
		text-align: center;
		font-weight: bold;
		font-size: 38upx;
	}

	.service-main-bottom {
		width: 100%;
		height: 100upx;
		font-size: 32upx;
		text-align: center;
		position: absolute;
		bottom: 0;
		color: #fff;
		background-color: #FD6801;
	}

	.service-main image {
		width: 40upx;
		height: 40upx;
		vertical-align: middle;
		margin-right: 10upx;
	}

	.description {
		font-weight: bold;
		font-size: 34upx;
	}

	.description-s {
		color: #BEBEBE;
		padding-left: 40upx;
	}
	.addresss{
		border-bottom: 2upx #EEE solid;
		width: 80%;
		margin: 0 auto;
		line-height: 50upx;
		text-align: left;
		position: relative;
	}
	.addresss>image{
		height: 50upx;
		width: 50upx;
		vertical-align: middle;
		display: inline-block;
		margin: 0!important;
		position: absolute;
		left: 20upx;
		top: 20upx;
	}
	.address-name{
		display: inline-block;
		font-size: 32upx;
		font-weight: bold;
		height: 50upx;
		width: 100%;
		text-align: left;
	}
	.address-city{
		font-size: 22upx;
		color: #999999;
		height: 50upx;
		margin-left: 30upx;
	}
	.comment {
		height: 500upx;
		width: 100%;
		white-space: nowrap;
		margin-bottom: 20upx;
	}

	.comment-list {
		background-color: #F5F5F3;
		border-radius: 20upx;
		height: 400upx;
		width: 550upx;
		display: inline-block;
		margin-right: 20upx;
		padding: 30upx 0 20upx 20upx;
		font-weight: bold;
	}

	.comment-list-tit image {
		width: 80upx;
		height: 80upx;
		border-radius: 50%;
		margin-right: 10upx;
	}

	.comment-list-txt {
		margin: 30upx 0;
	}

	.comment-list-img image {
		width: 300upx;
		height: 200upx;
	}

	.comment-list-tit-mid {
		display: inline-block;
		width: 300upx;
		height: 114upx;
		margin-left: 10upx;
	}

	.comment-list-tit-mid>view {
		color: #b9b9bf;
		font-size: 26upx;
	}

	.comment-list-tit-right {
		float: right;
		font-size: 26upx;
		color: #b9b9bf;
		line-height: 100upx;
		margin-right: 40upx;
	}

	.comment-list-tit-right>image {
		width: 35upx;
		height: 35upx;
		vertical-align: middle;
	}

	.more-comment {
		text-align: center;
		margin-bottom: 60upx;
	}

	.more-comment image {
		width: 50upx;
		height: 50upx;
		vertical-align: middle;
	}

	.recommended-to-you {
		font-size: 44upx;
		margin: 60upx 0 30upx 20upx;
	}

	.bottom {
		margin-bottom: 100upx;
		width: 100%;
		height: 2upx;
	}
</style>
