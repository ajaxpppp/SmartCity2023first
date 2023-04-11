<template>
	<view>
		<uni-section title="职位信息" sub-title="" type="line">
			<uni-card :title="`职位名称:${item.name}`">
				<view>岗位职责:{{item.obligation}}</view>
				<view>公司地点:{{item.address}}</view>
				<view>薪资待遇:{{item.salary}}</view>
				<view>联系人:{{item.contacts}}</view>
				<view>职位描述:{{item.professionName!=null?item.professionName:"暂无描述"}}</view>
				<view>职位需求:{{item.need}}</view>
			</uni-card>
		</uni-section>

		<uni-section title="公司名称" sub-title="" type="line">
			<uni-card>
				<view>公司简介:{{item2.introductory}}</view>
			</uni-card>
		</uni-section>

		<button type="primary" @click="addvitae">投简历</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				item: [],
				item2: [],
				user: [],
				curri: []
			}
		},
		methods: {
			addvitae() {
				if (this.curri.experience == null && this.curri.education == null) {
					uni.navigateTo({
						url: '/pages/job-hunting/curriculumvitae/curriculumvitae'
					})
				} else {
					this.$r.h(`/prod-api/api/job/deliver`, 'post', {
						"companyId": this.item2.id,
						"companyName": this.item2.companyName,
						"id": this.item2.id,
						"money": this.curri.money,
						"postId": this.curri.positionId,
						"postName": this.curri.positionName,
						"remark": "沈俊",
						"satrTime": this.$r.getDate(),
						"userId": this.user.userId,
						"userName": this.user.userName
					}).then(res => {
						uni.showToast({
							title: "投递成功"
						});
					})
				}
			}
		},
		onLoad(e) {
			this.$r.h(`/prod-api/api/job/post/${e.id}`).then(res => {
				this.item = res.data
			})

			this.$r.h(`/prod-api/api/job/company/${e.id}`).then(res => {
				this.item2 = res.data
			})



			this.$r.h(`/prod-api/api/common/user/getInfo`).then(res => {
				this.user = res.user
				if (res.code == 200) {
					this.$r.h(`/prod-api/api/job/resume/queryResumeByUserId/${this.user.userId}`).then(res => {
						this.curri = res.data
					})
				} else {
					uni.showToast({
						title: res.msg
					});
				}
			})

			this.$r.h(`/prod-api/api/job/deliver/list`).then(res => {
				console.log("res: " + JSON.stringify(res));
			})
		}
	}
</script>

<style>

</style>