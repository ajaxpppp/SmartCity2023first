<template>
	<view>
		<uni-segmented-control :current="current" :values="vitae" @clickItem="clickItem"></uni-segmented-control>
		<view class="content">
			<view v-show="current === 0">
				<uni-section title="查询简历" sub-title="" type="line">
					<uni-card title="基本信息">
						<uni-forms ref="form">
							<uni-forms-item label="用户昵称" label-width="75px">
								<uni-easyinput v-model="user.nickName" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="邮件" label-width="75px">
								<uni-easyinput v-model="user.email" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="电话号码" label-width="75px">
								<uni-easyinput v-model="user.phonenumber" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="性别" label-width="75px">
								<uni-easyinput v-model="user.sex==0?'女':'男'" placeholder="" />
							</uni-forms-item>
						</uni-forms>
					</uni-card>

					<uni-card title="求职信息">
						<uni-forms ref="form">
							<uni-forms-item label="工作经验" label-width="75px">
								<uni-easyinput v-model="curri.experience" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="最高学历" label-width="75px">
								<uni-easyinput v-model="curri.mostEducation" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="现居住地" label-width="75px">
								<uni-easyinput v-model="curri.address" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="期望职位" label-width="75px">
								<uni-easyinput v-model="positions.name" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="期望薪资" label-width="75px">
								<uni-easyinput v-model="curri.money" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="教育经历" label-width="75px">
								<uni-easyinput v-model="curri.education" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="个人简介" label-width="75px">
								<textarea name="" v-model="curri.individualResume" id=""
									style="width: 100%;"></textarea>
							</uni-forms-item>
						</uni-forms>
					</uni-card>
				</uni-section>
			</view>
			<view v-show="current === 1">
				<uni-section title="新增简历" sub-title="" type="line">
					<uni-card title="基本信息">
						<uni-forms ref="form">
							<uni-forms-item label="用户昵称" label-width="75px">
								<uni-easyinput v-model="user.nickName" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="邮件" label-width="75px">
								<uni-easyinput v-model="user.email" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="电话号码" label-width="75px">
								<uni-easyinput v-model="user.phonenumber" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="性别" label-width="75px">
								<uni-easyinput v-model="user.sex==0?'女':'男'" placeholder="" />
							</uni-forms-item>
						</uni-forms>
					</uni-card>

					<uni-card title="求职信息">
						<uni-forms ref="form">
							<uni-forms-item label="工作经验" label-width="75px">
								<uni-easyinput v-model="curri.experience" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="最高学历" label-width="75px">
								<uni-easyinput v-model="curri.mostEducation" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="现居住地" label-width="75px">
								<uni-easyinput v-model="curri.address" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="期望职位" label-width="75px">
								<uni-easyinput v-model="positions.name" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="期望薪资" label-width="75px">
								<uni-easyinput v-model="curri.money" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="教育经历" label-width="75px">
								<uni-easyinput v-model="curri.education" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="个人简介" label-width="75px">
								<textarea name="" v-model="curri.individualResume" id=""
									style="width: 100%;"></textarea>
							</uni-forms-item>
						</uni-forms>
						<button type="primary" @click="addvitae">新增简历</button>
					</uni-card>
				</uni-section>
			</view>
			<view v-show="current === 2">
				<uni-section title="编辑简历" sub-title="" type="line">
					<uni-card title="基本信息">
						<uni-forms ref="form">
							<uni-forms-item label="用户昵称" label-width="75px">
								<uni-easyinput v-model="user.nickName" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="邮件" label-width="75px">
								<uni-easyinput v-model="user.email" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="电话号码" label-width="75px">
								<uni-easyinput v-model="user.phonenumber" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="性别" label-width="75px">
								<uni-easyinput v-model="user.sex==0?'女':'男'" placeholder="" />
							</uni-forms-item>
						</uni-forms>
					</uni-card>

					<uni-card title="求职信息">
						<uni-forms ref="form">
							<uni-forms-item label="工作经验" label-width="75px">
								<uni-easyinput v-model="curri.experience" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="最高学历" label-width="75px">
								<uni-easyinput v-model="curri.mostEducation" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="现居住地" label-width="75px">
								<uni-easyinput v-model="curri.address" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="期望职位" label-width="75px">
								<uni-easyinput v-model="curri.positionId" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="期望薪资" label-width="75px">
								<uni-easyinput v-model="curri.money" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="教育经历" label-width="75px">
								<uni-easyinput v-model="curri.education" placeholder="" />
							</uni-forms-item>
							<uni-forms-item label="个人简介" label-width="75px">
								<textarea name="" v-model="curri.individualResume" id=""
									style="width: 100%;"></textarea>
							</uni-forms-item>
						</uni-forms>
						<button type="primary" @click="updatevitae">编辑简历</button>
					</uni-card>
				</uni-section>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				current: 0,
				user: [],
				vitae: ['查询', '新增', '编辑'],
				curri: [],
				positions: []
			}
		},
		methods: {
			addvitae() {
				this.$r.h(`/prod-api/api/job/resume`, 'post', {
					"id": this.curri.id,
					"mostEducation": this.curri.mostEducation,
					"education": this.curri.education,
					"address": this.curri.address,
					"experience": this.curri.experience,
					"individualResume": this.curri.individualResume,
					"money": this.curri.money,
					"positionId": this.curri.positionId,
					"files": null,
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: res.msg
						});
					} else {
						uni.showToast({
							title: res.msg
						});
					}
				})
			},
			clickItem(e) {
				this.current = e.currentIndex
			},
			updatevitae() {
				this.$r.h(`/prod-api/api/job/resume`, 'put', {
					"id": this.curri.id,
					"mostEducation": this.curri.mostEducation,
					"education": this.curri.education,
					"address": this.curri.address,
					"experience": this.curri.experience,
					"individualResume": this.curri.individualResume,
					"money": this.curri.money,
					"positionId": this.curri.positionId,
					"files": null,
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: "编辑成功"
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
			this.$r.h(`/prod-api/api/common/user/getInfo`).then(res => {
				this.user = res.user
				if (res.code == 200) {
					this.$r.h(`/prod-api/api/job/resume/queryResumeByUserId/${this.user.userId}`).then(res => {
						this.curri = res.data
						if (res.code == 200) {
							this.$r.h(`/prod-api/api/job/post/${this.curri.positionId}`)
								.then(
									res => {
										this.positions = res.data
									})
						}
					})
				} else {
					uni.showToast({
						title: res.msg
					});
				}
			})
		}
	}
</script>

<style>

</style>