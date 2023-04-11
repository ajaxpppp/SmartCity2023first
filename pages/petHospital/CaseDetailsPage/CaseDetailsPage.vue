<template>
	<view>
		<uni-list>
			<uni-list-item title="" note="">
				<template v-slot:body>
					<view style="display: flex;">
						<view>
							<image style="width: 320rpx; height: 220rpx; border-radius: 20rpx; margin-right: 20rpx;"
								:src="$u.a+item.doctor.avatar" mode=""></image>
						</view>
						<view>
							<view style="font-weight: bold;">医生姓名:{{item.doctor.name}}</view>
							<view>医生职称:{{item.doctor.jobName}}</view>
							<view>职业编号:{{item.doctor.practiceNo}}</view>
						</view>
					</view>
				</template>
			</uni-list-item>
			<view>咨询描述:{{item.doctor.goodAt}}</view>
			<uni-section title="问题图片" sub-title="" type="line">
				<image :src="$u.a+`/prod-api/`+item.imageUrls" style="" mode="">
				</image>
			</uni-section>
		</uni-list>

		<uni-section title="医生回复" sub-title="" type="line">
			<view style="text-align: center; font-size: 50rpx;">暂无回复</view>
		</uni-section>

		<navigator :url="`../Consultationpage/Consultationpage?id=${JSON.stringify(item)}`">
			<button type="primary">去提问</button>
		</navigator>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				item: [],
				list: [],
				pwd: ''
			}
		},
		methods: {
			login() {
				this.$r.h(`/prod-api/api/pet-hospital/inquiry-message`, 'post', {
					"inquiryId": this.item.id,
					"content": this.pwd
				}).then(res => {
					uni.showToast({
						title: res.msg,
					});
					this.pwd = ""

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