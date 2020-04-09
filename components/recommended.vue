<template name="recommended">
	<view>
		<view class="rec-commodity">
			<view v-for="(item,index) in recommended"  @click="details(item.id)" >
				<view class="rec-commodity-image">
					<image :src="item.cover" mode="" />
				</view>
				<view class="rec-commodity-title rec-commodity-txt">{{item.title}}</view>
				<view class="rec-commodity-desc  rec-commodity-txt">{{item.desc}}</view>
				<view class="rec-commodity-price rec-commodity-txt"> <text class="rec-commodity-price-y">￥</text>
					{{item.min_price}} <text class="rec-commodity-price-y" style="color:rgba(0,0,0,.54) ;"> ￥</text><text class="rec-commodity-min">
					{{item.min_oprice}}</text></view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"recommended",
		data() {
			return {
				recommended: [],
			}
		},
		created:function(e){
			uni.request({
				url: 'http://ceshi3.dishait.cn/api/goods/hotlist', 
				success: (res) => {
					this.recommended = res.data.data
				}
			});
		},
		methods: {
			details(e) {
				let id = e;
				console.log(id)
				uni.redirectTo({
					url: '../details/details?id=' + id,
					success(){
							 let page = getCurrentPages().pop(); 
					             if (!page) return;  
					             page.onLoad(id); 
						  }
				});
			}
		}
	}
</script>

<style scoped>
	.rec-commodity {}
	
	.rec-commodity>view {
		width: 49%;
		display: inline-block;
	}
	
	.rec-commodity>view:nth-child(odd) {
		margin-right: 1%;
	}
	
	
	.rec-commodity-txt {
		padding: 0 30upx;
	}
	
	.rec-commodity-image {
		position: relative;
		width: 100%;
		height: 0px;
		padding-top: 100%; 
	
	}
	
	.rec-commodity-image>image {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
	}
	
	.rec-commodity-title {
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
		font-size: 33upx;
		margin-top: 20upx;
	}
	
	.rec-commodity-desc {
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 1;
		font-size: 24upx;
		margin-top: 8upx;
	}
	
	.rec-commodity-price {
		color: red;
		margin-bottom: 20upx;
	}
	
	.rec-commodity-min {
		color: rgba(0, 0, 0, .54);
		font-size: 22upx;
		text-decoration: line-through;
	}
	
	.rec-commodity-price-y {
		font-size: 22upx;
		text-decoration: none;
		position: relative;
		top: -8upx;
	}
</style>
