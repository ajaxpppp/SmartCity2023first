<template>
	<view>
		<uni-section title="律师信息" sub-title="" type="line">
			<uni-card>
				<view style="display: flex;">
					<view>
						<image :src="$u.a+item.avatarUrl" style="width: 320rpx; height: 320rpx; margin-right: 20rpx;"
							mode=""></image>
					</view>
					<view>
						<view style="font-weight: bold;">{{item.name}}</view>
						<view>从业年限:{{item.workStartAt}}年</view>
						<view>咨询人数:{{item.serviceTimes}}人</view>
						<view>法律专长:{{item.legalExpertiseName}}</view>
						<view>好评率:{{item.favorableRate}}%</view>
					</view>
				</view>
			</uni-card>
		</uni-section>

		<uni-section title="问题信息填写" sub-title="" type="line">
			<uni-forms ref="form" style="margin: 100rpx;">
				<uni-forms-item label="问题类型" name="">
					<button style="margin: -10rpx;" type="primary" plain="" @click="clicklist">点击选择问题类型</button>
				</uni-forms-item>
				<uni-forms-item label="问题描述" name="">
					<uni-easyinput v-model="content" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="上传的图片" name="">
					<image @click="img" :src="$u.a+`/prod-api/`+imageUrls"
						style="border-radius: 20rpx; width: 100%; height: 200rpx; border: 1px solid;">
					</image>
				</uni-forms-item>
				<uni-forms-item label="联系电话" name="">
					<uni-easyinput v-model="phone" placeholder="" />
				</uni-forms-item>
				<button type="primary" style="margin: 50rpx;" @click="commit">评论</button>
			</uni-forms>
		</uni-section>

		<uni-popup ref="popup" type="center">
			<uni-popup-message v-if="temp==true">
				<uni-section title="全部法律专长列表" sub-title="" type="line">
					<scroll-view scroll-y="true" style="width:720rpx; height: 600rpx;">
						<uni-grid :column="4" :showBorder="false">
							<uni-grid-item v-for="(item,index) in icon" :key="index" style="width: 25%;">
								<view @click="selectService(item.id)" class="imgs" style="font-size: 18rpx;">
									<image style="width: 80rpx; height: 80rpx; border-radius: 50%;"
										:src="$u.a+item.imgUrl" mode=""></image>
									<view>{{item.name}}</view>
								</view>
							</uni-grid-item>
						</uni-grid>
					</scroll-view>
				</uni-section>
			</uni-popup-message>
		</uni-popup>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				temp: false,
				item: [],
				"lawyerId": "",
				"legalExpertiseId": "",
				"content": "",
				"imageUrls": "",
				"phone": "",
				icon: [],
				lawyer: 0

			}
		},
		methods: {
			clicklist() {
				this.$refs.popup.open()
				this.temp = true
			},
			commit() {
				this.$r.h(`/prod-api/api/lawyer-consultation/legal-advice`, 'post', {
					"lawyerId": this.item.id,
					"legalExpertiseId": this.lawyer,
					"content": this.content,
					"imageUrls": this.imageUrls,
					"phone": this.phone,
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: res.msg
						});
						this.item.id = ""
						this.lawyer = ""
						this.content = ""
						this.imageUrls = ""
						this.phone = ""
						uni.navigateBack({
							delta: 1
						});
					} else {
						uni.showToast({
							title: res.msg
						});
					}

				})
			},
			selectService(e) {
				this.lawyer = e
				this.temp = false
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
								this.imageUrls = images.fileName
							}
						})
					}
				})
			}
		},
		onLoad(e) {
			this.$r.h(`/prod-api/api/lawyer-consultation/legal-expertise/list`).then(res => {
				this.icon = res.rows.sort(function(a, b) {
					return b.sort - a.sort
				})
			})
			this.item = JSON.parse(e.id)
		}
	}
</script>

<style>

</style>