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
				<image :src="$u.a+`/prod-api/`+item.imageUrls" mode=""></image>
			</uni-section>
		</uni-list>

		<view style="height: 20rpx;"></view>
		<uni-section title="问答列表" sub-title="" type="line">
			<view v-for="(item,index) in commit" :key="index" style="margin: 70rpx;">
				<view>{{item.fromRole==1?`宠物医生:${item.fromId}`:`就诊人用户:${item.fromId}`}}</view>
				<view>内容:{{item.content}}</view>
				<view style="display: flex; width: 100%;">
					<uni-forms-item label="输入问题" name="">
						<uni-easyinput style="width:400rpx;" v-model="question" placeholder="" />
						<button type="primary" @click="add(item.id)">发送</button>
					</uni-forms-item>
				</view>
			</view>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				question: "",
				item: [],
				list: [],
				pwd: '',
				commit: [],
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
			},
			add(e) {
				this.$r.h(`/prod-api/api/pet-hospital/inquiry-message`, 'post', {
					"inquiryId": e,
					"content": this.question
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: res.msg
						});
						this.$r.h(`/prod-api/api/pet-hospital/inquiry-message/list?inquiryId=${this.id}`).then(
							res => {
								this.commit = res.rows
							})
						this.question = ""
					}
				})
			}
		},
		onLoad(e) {
			this.item = JSON.parse(e.id)
			this.id = this.item.doctor.id
			this.$r.h(`/prod-api/api/pet-hospital/inquiry-message/list?inquiryId=${this.id}`).then(res => {
				this.commit = res.rows
			})
		}
	}
</script>

<style>

</style>