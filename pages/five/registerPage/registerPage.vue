<template>
	<view>
		<uni-forms ref="form" style="padding:70rpx;">
			<!-- <uni-forms-item label="头像" name="">
				<image @click="img" style="border: 1px solid; width: 220rpx; height: 200rpx; border-radius: 50%;">
				</image>
			</uni-forms-item> -->
			<uni-forms-item label="用户名">
				<uni-easyinput v-model="user.userName" placeholder="请输入用户名" />
			</uni-forms-item>
			<!-- <uni-forms-item label="昵称" name="">
				<uni-easyinput v-model="user.nickName" placeholder="请输入昵称" />
			</uni-forms-item> -->
			<uni-forms-item label="密码">
				<uni-easyinput v-model="user.password" placeholder="请输入密码" type="password" />
			</uni-forms-item>
			<uni-forms-item label="电话号码">
				<uni-easyinput v-model="user.phonenumber" placeholder="请输入11位电话号码" />
			</uni-forms-item>
			<uni-forms-item label="性别">
				<uni-data-checkbox :localdata="localdata" v-model="value"></uni-data-checkbox>
			</uni-forms-item>
			<!-- <uni-forms-item label="邮箱">
				<uni-easyinput v-model="user.email" placeholder="请以xx@qq.com格式输入" />
			</uni-forms-item> -->
			<!-- <uni-forms-item label="身份证">
				<uni-easyinput v-model="user.idCard" placeholder="请以身份证格式输入" />
			</uni-forms-item> -->
			<button type="primary" @click="change">注册</button>
		</uni-forms>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				user: {
					"avatar": " ",
					"userName": "",
					"nickName": "",
					"password": "",
					"phonenumber": "",
					"sex": "0",
					"email": "",
					"idCard": ""
				},
				localdata: [{
						text: '男',
						value: '0'
					},
					{
						text: '女',
						value: '1'
					}
				],
				value: 0,
			}
		},
		methods: {
			// img() {
			// 	uni.chooseImage({
			// 		count: 1,
			// 		success: (res) => {
			// 			uni.uploadFile({
			// 				url: this.$u.a + "/prod-api/common/upload",
			// 				method: 'post',
			// 				name: "file",
			// 				header: {
			// 					Authorization: uni.getStorageSync("token")
			// 				},
			// 				filePath: res.tempFilePaths[0],
			// 				success: res => {
			// 					let images = JSON.parse(res.data)
			// 					this.user.avatar = images.fileName
			// 					console.log("res: " + JSON.stringify(res));
			// 					console.log(": " + JSON.stringify(uni.getStorageSync("token")));
			// 				}
			// 			})
			// 		}
			// 	})
			// },
			change() {
				this.$r.h(`/prod-api/api/register`, 'post', {
					// "avatar": this.user.avatar,
					"userName": this.user.userName,
					// "nickName": this.user.nickName,
					"password": this.user.password,
					"phonenumber": this.user.phonenumber,
					"sex": this.value,
					// "email": this.user.email,
					// "idCard": this.user.idCard,
				}).then(res => {
					console.log("res: " + JSON.stringify(res));
					if (res.code == 200) {
						uni.showToast({
							title: res.msg + "快去登录吧"
						});
						setTimeout(() => {
							uni.reLaunch({
								url: '/pages/five/login/login'
							})
						}, 3000)

					} else {
						uni.showToast({
							title: res.msg
						});
					}
				})
			},
		}
	}
</script>

<style>

</style>
