<template>
	<view class="box">
		<view class="top">
			<block v-for="item in condition">
				<view class="con-box dis">
					<view class="comm-nam">{{item}}</view>
					<view class="caret ">
						<view class="caretimg"style="margin-top: 10%;"><image src="../../static/xie/caret-top.png"></image></view>
						<view class="caretimg"><image src="../../static/xie/caret-bottom.png"></image></view>
					</view>
				</view>
			</block>
			<view class="con-box">
				<text class="shaix" @click="zhaoShow">筛选</text>
			</view>
		</view>
		<view class="nocomm" v-show="nocomm">什么都没有......</view>
	 <!-- 商品 -->
		<view class="cooks ">
			<scroll-view scroll-y="true" style="height: 990upx;">
				<block  v-for="(item,index) in paren">
				<view class="cooks-box bor-bottom">
					<view class="cooks-img "><image :src="item.cover" ></image></view>
					<view class="cooks-tet ">
						<view class="fontsty1 ">{{item.title}}</view>
						<view class="fontsty2 text-overflows ">{{item.desc}}</view>
						<view class="fontsty3 ">¥{{item.min_price}}</view>
						<view class="fontsty2 ">1348条评论 66%满意度</view>
					</view>
				</view>
				</block>
			</scroll-view>
		</view>
		<!-- 防尘罩 -->
		<view class="zhao" v-show="zhao">
			<view class="zhao-box">
				<view class="zhao-tit">服务</view>
				<view class="claname">
					<block v-for="(item,index) in servename" :key="index">
						<text :class="[serveind===index?'bgsty':'namesty']" @click="newServeind(index)">{{item}}</text>
					</block>
				</view>
				<view class="zhao-tit">分类</view>
				<view class="claname">
					<block v-for="(ite,index) in claname" :key="index">
						<text :class="[claind===index?'bgsty':'namesty']"  @click="newClaind(index)">{{ite}}</text>
					</block>
				</view>
				<view class="bot-btn">
					<view class="oldsty" @click="oldsty">重置</view>
					<view class="newsty" @click="newsty">确定</view>
				</view>
			</view>
		</view>
	
	</view>
</template>

<script>
	export default{
		props:["paren","nocomm"],
		data(){
			return{
				condition:["综合","销量","价格"],
				servename:["特价","分期","仅看有货"],
				claname:["耳机","手机","手表"],
				eData:[],
				zhao:false,
				claind:0,
				serveind:0
			}
		},
		onLoad(){
			
			console.log(this.paren)
		},
		
		methods:{
			newServeind(ind){
				console.log(ind)
				this.serveind=ind
			},
			newClaind(ind){
				this.claind=ind
			},
			oldsty(){
				this.serveind=0;
				this.claind=0
			},
			newsty(){
				this.zhao=false
			},
			zhaoShow(){
				this.zhao=!this.zhao
			}
		}
	}
</script>

<style scoped>
.box{width: 99%;margin: auto;}
.bor{border: 1upx solid #DD524D;}
.dis{display: flex;}
.top{border: 1upx solid #CCCCCC;height: 80upx;display: flex;width: 100%;border-width: 1upx 0;}
.con-box{width:25%;height: 100%;font-size: 35upx;}
.comm-nam{width:70%;height: 100%;line-height: 80upx;text-align: right;}
.caret{width:25%;height: 100%;}
.caretimg{width: 70%;height:40%;}
.caretimg>image{width:100%;height:100%;}
.shaix{color:#DD524D;line-height: 80upx;margin-left:50upx;}
/* 商品 */
.cooks{width: 100%;margin-top:10upx;}
.bor-bottom{border-bottom: 2upx solid #C8C7CC;}
.cooks-box{width: 96%;margin: 0 auto;height: 300upx;display: flex;margin-top: 20upx;padding-bottom: 20upx;}
.cooks-img{width: 35%;height: 100%;}
.cooks-img>image{width: 100%;height:100%;}
.cooks-tet{width:62%;margin-left: 3%;}
.fontsty1{font-weight: bold;height: 70upx;line-height: 70upx;}
.fontsty2{font-size: 28upx;height: 70upx;line-height: 35upx;color: #666666;}
.fontsty3{color: #DD524D;height: 90upx;line-height: 90upx;font-size: 38upx;}
.nocomm{width: 100%;margin-top:300upx;color: #CCCCCC;font-size: 40upx;text-align: center;}
.text-overflows{
    display: -webkit-box;    
    -webkit-box-orient: vertical;    
    -webkit-line-clamp: 2;    
    overflow: hidden;
}
.box>.zhao{width: 100%;height:83%;position: absolute; background:rgba(0,0,0,.3);top:17%;}
.zhao-box{width: 80%;height: 100%;background: #FFFFFF;float: right;position: relative;}
.zhao-tit{line-height: 80upx;height: 80upx;margin: 30upx;}
.namesty{padding: 10upx 30upx;margin: 0 20upx;background: #F8F9FB;}
.bgsty{background: #FCE0D5;border: 1upx solid #F0AD4E;color: #DD524D;padding: 10upx 20upx;margin: 0 20upx;}
.zhao-box>.bot-btn{width: 100%;height: 100upx;line-height: 100upx;display: flex;position: absolute;bottom: 1upx;}
.bot-btn{text-align: center;}
.newsty{background:#F0AD4E;color: #F8F8F8;width: 50%;}
.oldsty{background: #F8F9FB;width: 50%;}
</style>
