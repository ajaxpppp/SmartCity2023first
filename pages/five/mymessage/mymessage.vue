<template>
	<view>
		<uni-forms ref="form" style="padding: 100rpx;">
			<uni-forms-item label="头像" name="">
				<image @click="img" :src="$u.a+`/prod-api/`+user.avatar"
					style="width: 220rpx; height: 200rpx; border-radius: 50%;">
				</image>
			</uni-forms-item>
			<uni-forms-item label="昵称">
				<uni-easyinput v-model="user.nickName" placeholder="" />
			</uni-forms-item>
			<uni-forms-item label="性别" name="">
				<uni-data-checkbox :localdata="localdata" v-model="value"></uni-data-checkbox>
			</uni-forms-item>
			<uni-forms-item label="联系电话">
				<uni-easyinput v-model="user.phonenumber" placeholder="" />
			</uni-forms-item>
			<button type="primary" @click="change">修改</button>
		</uni-forms>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				value: null,
				user: [],
				localdata: [{
					text: '男',
					value: '0'
				}, {
					text: '女',
					value: '1'
				}]
			}
		},
		methods: {
			change() {
				this.$r.h(`/prod-api/api/common/user`, 'put', {
					avatar: this.user.avatar,
					nickName: this.user.nickName,
					sex: this.value,
					phonenumber: this.user.phonenumber
				}).then(res => {
					console.log("res: " + JSON.stringify(res));
					if (res.code == 200) {
						this.$r.h(`/prod-api/api/common/user/getInfo`).then(res => {
							uni.setStorageSync("user", res.user)
						})
						uni.reLaunch({
							url: '/pages/five/five'
						})
					} else {
						uni.showToast({
							title: res.msg
						});
					}
				})
			},
			img() {
				uni.chooseImage({
					count: 1,
					success: (res) => {
						uni.uploadFile({
							url: this.$u.a + "/prod-api/common/upload",
							method: 'post',
							name: "file",
							header: {
								Authorization: uni.getStorageSync("token")
							},
							filePath: res.tempFilePaths[0],
							success: res => {
								let images = JSON.parse(res.data)
								this.user.avatar = images.fileName
							}
						})
					}
				})
			}
		},
		onLoad() {
			this.$r.h(`/prod-api/api/common/user/getInfo`).then(res => {
				this.user = res.user
				this.value = this.user.sex
				this.user.phonenumber = this.user.phonenumber.substring(0, 7) + "****"
			})
		}
	}
</script>

<style>

</style>
