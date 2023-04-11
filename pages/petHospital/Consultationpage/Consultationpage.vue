<template>
	<view>
		<uni-section title="医生信息" sub-title="" type="line">
			<uni-list>
				<uni-list-item title="" note="">
					<template v-slot:body>
						<view style="display: flex;">
							<view>
								<image style="width: 320rpx; height: 220rpx; border-radius: 20rpx; margin-right: 20rpx;"
									:src="$u.a+item.avatar" mode=""></image>
							</view>
							<view>
								<view style="font-weight: bold;">医生姓名:{{item.name}}</view>
								<view>职称:{{item.jobName}}</view>
								<view>职业编号:{{item.practiceNo}}</view>
								<view>从业年限:{{item.workingYears}}</view>
								<view>擅长描述:{{item.goodAt?item.goodAt.slice(0,10)+"...":""}}</view>
							</view>
						</view>
					</template>
				</uni-list-item>
			</uni-list>

			<uni-forms ref="form" style="margin: 50rpx;">
				<uni-forms-item label="图片" name="">
					<button type="primary" @click="img">上传图片</button>
				</uni-forms-item>
				<uni-forms-item label="问题描述" name="">
					<textarea v-model="pwd" maxlength="150" style="width: 100%; border: 1px solid;" placeholder="" />
					字数:{{pwd.length}}
				</uni-forms-item>
				<button type="primary" @click="login">提交</button>
			</uni-forms>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				item: [],
				pwd: "",
				imgs: ""
			}
		},
		methods: {
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
								this.imgs = images.fileName
							}
						})
					}
				})
			},
			login() {
				this.$r.h(`/prod-api/api/pet-hospital/inquiry`, 'post', {
					"doctorId": this.item.id,
					"question": this.pwd,
					"imageUrls": this.imgs
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: res.msg
						});
						uni.navigateTo({
							url: '/pages/petHospital/petHospital',
						});
					} else {
						uni.showToast({
							title: res.msg
						});
					}
				})
			}
		},
		onLoad(e) {
			this.item = JSON.parse(e.id)
		}
	}
</script>

<style>

</style>