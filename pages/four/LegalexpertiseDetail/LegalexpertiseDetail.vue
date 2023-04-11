<template>
	<view>
		<uni-card>
			<view style="display: flex;">
				<view>
					<image :src="$u.a+item.avatarUrl" style="width: 320rpx; height: 320rpx; margin-right: 20rpx;"
						mode=""></image>
				</view>
				<view>
					<view style="font-weight: bold;">{{item.name}}</view>
					<view>法律专长:{{item.legalExpertiseName}}</view>
					<view>咨询人数:{{item.serviceTimes}}人</view>
					<view>服务次数:{{item.favorableCount}}次</view>
				</view>
			</view>
		</uni-card>
		<uni-section title="tab页" sub-title="" type="line">
			<uni-segmented-control :current="current" :values="values" @clickItem="clickItem"></uni-segmented-control>
			<view class="content">
				<view v-show="current === 0">
					<!-- <image v-if="" style="border: 1px solid ;" :src="$u.a+item.certificateImgUrl" mode=""></image> -->
					<image src="../../../static/lawyer/lawyerphoto.jpg" mode=""></image>
					<view style="height: 50rpx;"></view>
					<uni-section title="个人简介" sub-title="" type="line">
						<view>{{item.baseInfo}}</view>
					</uni-section>
					<view style="height: 50rpx;"></view>
					<uni-section title="教育背景" sub-title="" type="line">
						<view>{{item.eduInfo}}</view>
						<view style="text-align: right; margin-top: 50rpx; font-weight: bold; font-size: 50rpx;">
							从业年限:{{item.workStartAt}}年</view>
						<view style="text-align: right;  font-weight: bold; font-size: 30rpx;">执业证号:{{item.licenseNo}}
						</view>
					</uni-section>
				</view>
				<view v-show="current === 1">
					<view v-for="(item,index) in list.slice(0,3)" :key="index">
						<uni-card>
							<view style="display: flex;">
								<view>
									<image :src="$u.a+`/prod-api/`+item.fromUserAvatar"
										style="width: 320rpx; height: 320rpx; margin-right: 20rpx;" mode=""></image>
								</view>
								<view>
									<view style="font-weight: bold;">{{item.title}}</view>
									<view>昵称:{{item.fromUserName}}</view>
									<view>评价时间:{{item.createTime}}</view>
									<view>评价内容:{{item.evaluateContent?item.evaluateContent.slice(0,10)+"...":""}}
									</view>
									<view>点赞数量:{{item.likeCount}}</view>
									<button type="primary" size="mini"
										@click="help(item.myLikeState,item.adviceId)">点赞</button>
								</view>
							</view>
						</uni-card>
					</view>
					<navigator
						:url="`../LegalexpertiseFreeGuidance/LegalexpertiseFreeGuidance?id=${JSON.stringify(item)}`"
						style="height: 100%;">
						<button type="primary">免费咨询</button>
					</navigator>
				</view>
			</view>
		</uni-section>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				item: [],
				values: ['服务方式', '用户评价'],
				current: 0,
				list: [],
				id: 0
			}
		},
		methods: {
			clickItem(e) {
				this.current = e.currentIndex
			},
			help(e, v) {
				if (e == false) {
					this.$r.h(`/prod-api/api/lawyer-consultation/legal-advice/evaluate-like`, 'post', {
						"adviceId": v,
						"like": !e
					}).then(res => {
						uni.showToast({
							title: "点赞"
						});
						this.$r.h(`/prod-api/api/lawyer-consultation/lawyer/list-evaluate?lawyerId=${this.id}`)
							.then(
								res => {
									this.list = res.rows.sort(function(a, b) {
										return b.createTime > a.createTime ? 1 : -1
									})
								})
					})
				} else {
					this.$r.h(`/prod-api/api/lawyer-consultation/legal-advice/evaluate-like`, 'post', {
						"adviceId": v,
						"like": !e
					}).then(res => {
						uni.showToast({
							title: "取消点赞"
						});
						this.$r.h(`/prod-api/api/lawyer-consultation/lawyer/list-evaluate?lawyerId=${this.id}`)
							.then(
								res => {
									this.list = res.rows.sort(function(a, b) {
										return b.createTime > a.createTime ? 1 : -1
									})
								})
					})
				}
			}
		},
		onLoad(e) {
			this.id = e.id
			this.$r.h(`/prod-api/api/lawyer-consultation/lawyer/${e.id}`).then(res => {
				this.item = res.data
				let date = new Date()
				this.item.workStartAt = parseInt(date.getFullYear()) - parseInt(this.item.workStartAt.slice(0,
					4))
			})

			this.$r.h(`/prod-api/api/lawyer-consultation/lawyer/list-evaluate?lawyerId=${this.id}`).then(res => {
				this.list = res.rows.sort(function(a, b) {
					return b.createTime > a.createTime ? 1 : -1
				})
			})
		}
	}
</script>

<style>

</style>