<template>
	<view>
		<view class="imgs" style="margin-top: 50rpx;">
			<image :src="$u.a+`/prod-api/`+user.avatar" style="width: 320rpx; height: 250rpx; border-radius: 50%;">
			</image>
			<view style="font-size: 35rpx;">昵称:{{user.nickName}}</view>
		</view>

		<navigator url="mymessage/mymessage" style="padding: 50rpx; font-size: 40rpx;">
			<view>
				<uni-icons type="person" size="25"></uni-icons> 个人信息
			</view>
		</navigator>
		<navigator url="passwd/passwd" style="padding: 50rpx; font-size: 40rpx;">
			<view>
				<uni-icons type="gear" size="25"></uni-icons>修改密码
			</view>
		</navigator>
		<navigator url="orderList/orderList" style="padding: 50rpx; font-size: 40rpx;">
			<view>
				<uni-icons type="compose" size="25"></uni-icons>订单列表
			</view>
		</navigator>
		<navigator url="inputList/inputList" style="padding: 50rpx; font-size: 40rpx;">
			<view>
				<uni-icons type="plusempty" size="25"></uni-icons>意见反馈
			</view>
		</navigator>
		<button type="primary" style="margin:60rpx;" @click="outlogin">退出登录</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				user: []
			}
		},
		methods: {
			outlogin() {
				uni.removeStorageSync("token")
				uni.reLaunch({
					url: '/pages/five/login/login'
				})
			}
		},
		onLoad() {
			this.$r.h(`/prod-api/api/common/user/getInfo`).then(res => {
				this.user = res.user
				uni.setStorageSync("user", this.user)
			})
		}
	}
</script>

<style>

</style>
