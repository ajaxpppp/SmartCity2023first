<template>
	<view>
		<view style="display: flex; position: relative; top:200rpx">
			<uni-forms ref="form" style="display: block; width: 100%; margin: 100rpx;">
				<uni-forms-item label="旧密码" name="">
					<uni-easyinput v-model="username" placeholder="请输入旧密码" />
				</uni-forms-item>
				<uni-forms-item label="新密码" name="">
					<uni-easyinput v-model="password" placeholder="请输入新密码" />
				</uni-forms-item>
				<button type="primary" style="margin: 50rpx;" @click="login">确定</button>
			</uni-forms>
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
			login() {
				this.$r.h(`/prod-api/api/common/user/resetPwd`, 'put', {
					"oldPassword": this.username,
					"newPassword": this.password
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: res.msg,
							success: () => {
								uni.switchTab({
									url: '/pages/five/five'
								})
							}
						});
					} else {
						uni.showToast({
							title: res.msg
						});
					}
				})
			}
		},
		onLoad() {

		}
	}
</script>

<style>

</style>
