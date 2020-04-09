<template>
	<view class="alter_info">
		<!-- 用户资料头像 -->
		<view class="head_pic bg-color">
			<view class="text">
				头像
			</view>
			<view class="user_pic">
				<image :src="userPic" mode=""></image>
			</view>
		</view>
		<!-- 姓名 -->
		<view class="name bg-color">
			<view class="text">
				姓名
			</view>
			<view class="search select">
				<input type="text" value=""   placeholder="输入姓名"/>
			</view>
			<view class="right">
				<image src="../../static/tan/right.png" mode=""></image>
			</view>
		</view>
		<!-- 性别 -->
		<view class="sex bg-color">
			<view class="text">
				性别
			</view>
			<view class="sex_select select">
				<picker @change="bindPickerChange" :value="index" :range="array">
					<view class="uni-input">{{array[index]}}</view>
				</picker>
			</view>
			<view class="right">
				<image src="../../static/tan/right.png" mode=""></image>
			</view>
		</view>
		<!-- 生日 -->
		<view class="birthday">
			<view class="text">
				生日
			</view>
			<view class="select_date select">
				<picker mode="date" :value="date" :start="startDate" :end="endDate" @change="bindDateChange">
					<view class="uni-input">{{date}}</view>
				</picker>
			</view>
			<view class="right">
				<image src="../../static/tan/right.png" mode=""></image>
			</view>
		</view>
		<!-- 修改密码 -->
		<view class="change_pwd bg-color">
			<view class="text">
				修密码
			</view>
			<view class="right">
				<image src="../../static/tan/right.png" mode=""></image>
			</view>
		</view>
		<!-- 密保手机 -->
		<view class="birthday">
			<view class="text">
				密保手机
			</view>
			<view class="right">
				<image src="../../static/tan/right.png" mode=""></image>
			</view>
		</view>
	</view>
	</view>
</template>

<script>
	export default {
		data() {
			const currentDate = this.getDate({
				format: true
			})
			return {
				userPic: '',
				index: 0,
				date: currentDate,
				array: ['男', '女']
			}
		},
		methods: {
			bindPickerChange: function(e) {
				this.index = e.target.value
			},
			bindDateChange: function(e) {
				this.date = e.target.value
			},
			getDate(type) {
				const date = new Date();
				let year = date.getFullYear();
				let month = date.getMonth() + 1;
				let day = date.getDate();

				if (type === 'start') {
					year = year - 60;
				} else if (type === 'end') {
					year = year + 2;
				}
				month = month > 9 ? month : '0' + month;;
				day = day > 9 ? day : '0' + day;
				return `${year}-${month}-${day}`;
			}
		},
		onLoad() {
			uni.request({
				url: 'http://ceshi3.dishait.cn/api/login',
				method: 'POST',
				data: {
					username: 'user2',
					password: 'zcmcss'
				},
				success: (res) => {
					this.userPic = res.data.data.avatar
				}
			});
		},
		computed: {
			startDate() {
				return this.getDate('start');
			},
			endDate() {
				return this.getDate('end');
			}
		}
	}
</script>

<style scoped>
	.alter_info {
		font-size: 30upx;
		overflow: hidden;
	}

	.alter_info>view {
		position: relative;
	}

	.bg-color {
		background-color: #FFFFFF;
		border-bottom: 1upx solid #CCCCCC;
	}

	.alter_info {
		width: 100%;
		height: 100%;
		background-color: #EEEEEE;
	}

	.head_pic {
		width: 100%;
		height: 150upx;
		line-height: 150upx;
		border-top: 20upx solid #EEEEEE;
		overflow: hidden;
	}

	.head_text {
		text-indent: 30upx;
		float: left;
	}

	.user_pic {
		float: right;
	}

	.user_pic image {
		width: 100upx;
		height: 100upx;
		border-radius: 50%;
		margin-top: 25upx;
		margin-right: 30upx;
	}
	.search input {
		width: 100%;
		height: 100%;
		color:#000000;
		text-shadow:0 0 0 black;
		text-align: right;
	}
	.name {
		width: 100%;
		height: 100upx;
		line-height: 100upx;
	}
	.select {
		width: 60%;
		height: 100%;
	}
	.uni-input{
		width: 100%;
	}
	.name view {
		float: left;
	}

	.sex {
		width: 100%;
		height: 100upx;
		line-height: 100upx;
	}

	.sex view {
		float: left;
	}

	.birthday {
		width: 100%;
		height: 100upx;
		line-height: 100upx;
		background-color: #FFFFFF;
		overflow: hidden;
	}

	.birthday view {
		float: left;
	}

	.change_pwd {
		width: 100%;
		height: 100upx;
		line-height: 100upx;
		margin-top: 20upx;
		overflow: hidden;
	}

	.text {
		width: 20%;
		text-indent: 20upx;
		float: left;
	}

	.right {
		width: 15%;
		height: 100%;
		text-align: right;
		margin-right: 30upx;
		position: absolute;
		right: 0;
		top: 8upx;
	}

	.right image {
		width: 35upx;
		height: 35upx;
	}
</style>
