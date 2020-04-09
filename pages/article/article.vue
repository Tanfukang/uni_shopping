<template>
	<view class="container">
		<view class="nav">
			<view>
				<text>小米商城</text>
			</view>
			<image src="../../static/gouwuche.png"></image>
		</view>
		<view class="box">
			<view class="introduce">Redmi K20 Pro常见购机咨询</view>
			<view class="partake">
				<view class="pre-sales">售前咨询:</view>
				<view class="ask">
					<view>1.怎么参与Redmi K20 Pro订金预售？</view>
					<view>答：订金预售活动在5月28日10:00开启，成功支付订金后即表示成功预订Redmi K20 Pro手机。点击“我的” - “代付款” 即可进行尾款支付，尾款支付时间在6月1日0点至24点。</view>
				</view>
				<view class="Depositrefund">
					<view>2.订金预售的订金可以退还吗？</view>
					<view>答：支付100元订金后，还可以申请退款，退款将在财务审核后及时退回</view>
				</view>
				<view class="charger">
					<view>3.Redmi K20 Pro标配什么充电器？</view>
					<view>答：原装标配18W充电器。Redmi K20 Pro最高可支持27W有线快充，如有需要，可自行选购。</view>
				</view>
				<view class="coordinates">
					<view>4.Redmi K20 Pro有哪些套装可以购买？</view>
					<view>答：在售套装有：</view>
					<view>(1) Redmi K20 Pro + Redmi 20寸红色旅行箱套装。旅行箱原价299元，套装内现价价格199元，还在等什么，现在快来抢购吧！</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data:{
		return:{
			
		}
	},
		methods: {

		},
	}
</script>

<style>
	.container {
		width: 100%;
	}

	/* 导航栏 */
	.nav {
		width: 100%;
		margin: auto;
		height: 80upx;
		background: #FAFAFA;
		line-height: 80upx;
		border-bottom: 5upx solid #F4F4F4;
	}

	.nav view {
		padding-left: 30upx;
		float: left;
	}

/* 	.nav view image {
		width: 40upx;
		height: 40upx;
		margin-top: 10upx;
		float: left;
		margin-top: 18upx;
	} */

	.nav image {
		width: 60upx;
		height: 60upx;
		float: right;
		margin-top: 8upx;
		padding-right: 30upx;
	}

	.nav view text {
		font-size: 35upx;
		display: inline-block;
		margin-top: 10upx;
		height: 40upx;
		line-height: 40upx;
		padding-left: 20upx;
	}

	/* 介绍商品以及问题 */
	.box {
		width: 90%;
		height: 800upx;
		margin: auto;
	}

	.box .introduce {
		font-size: 50upx;
		font-weight: 600;
	}

	.introduce {
		padding: 40upx 0upx;
	}

	/* 售前咨询 */
	.pre-sales {
		font-size: 30upx;
		font-weight: 800;
	}
		/* 怎么参与订金预售 */
	.ask {
		width: 100%;
		padding-top: 7upx;
	}

	.ask view {
		font-size: 30upx;
		line-height: 55upx;
	}
/* 押金是否可以退还 */
	.Depositrefund {
		width: 100%;
		padding-top: 30upx;
	}
	.Depositrefund view {
		font-size: 30upx;
		line-height: 55upx;
	}
	/* 标配充电器 */
	.charger {
		width: 100%;
		padding-top: 30upx;
	}
	.charger view {
		font-size: 30upx;
		line-height: 55upx;
	}
	/* 在售套装 */
	.coordinates{
		width: 100%;
		padding-top: 30upx;
	}
	.coordinates view {
		font-size: 30upx;
		line-height: 55upx;
		}
</style>
