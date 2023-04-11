<template>
	<view>
		<image src="../../../static/login/smartphoto.png"
			style="display: flex; position: relative; width: 100%; height:300rpx; " mode="">
		</image>
		<view style="display: flex; position: relative; top:-50rpx;">
			<uni-forms ref="form" style="display: block; width: 100%; margin: 100rpx;">
				<uni-forms-item label="用户名" name="">
					<uni-easyinput v-model="username" placeholder="请输入用户名" />
				</uni-forms-item>
				<uni-forms-item label="密码" name="">
					<uni-easyinput v-model="password" type="password" placeholder="请输入密码" />
				</uni-forms-item>
				<button type="primary" style="margin: 50rpx;" @click="login">登录</button>
			</uni-forms>

		</view>
		<view style="display: flex; justify-content: space-around;position: relative; top: -150rpx; color: gray">
			<view @click="register">注册账号</view>
			<view @click="warring" style="text-decoration: underline;"> 忘记密码?</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				username: "",
				password: ""
			}
		},
		methods: {
			warring() {
				uni.showToast({
					title: '功能正在开发中'
				});
			},
			register() {
				uni.navigateTo({
					url: '/pages/five/registerPage/registerPage'
				})
			},
			login() {
				this.$r.hs(`/prod-api/api/login`, 'post', {
					'username': this.username,
					'password': this.password
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: res.msg,
							success: () => {
								uni.setStorageSync("token", res.token)
								uni.switchTab({
									url: '/pages/index/index'
								})
							}
						});
					} else {
						uni.showToast({
							title: res.msg,
						});
					}
				})
			}
		},
		onLoad() {
			if (uni.getStorageSync("token") != "") {
				uni.switchTab({
					url: '/pages/index/index'
				})
			}
		}
	}
</script>

<style>

</style>
