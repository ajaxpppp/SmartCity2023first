<template>
	<view>
		<uni-search-bar placeholder="请输入律师名字" @confirm="confirm"></uni-search-bar>

		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,index) in sp" :key="index">
				<image :src="$u.a+item.imgUrl" style="width: 100%; height: 100%;"></image>
			</swiper-item>
		</swiper>

		<uni-section title="法律专长" sub-title="" type="line">
			<view>
				<swiper style="height: 30vh;" :indicator-dots="true">
					<swiper-item>
						<uni-grid :column="4" :showBorder="false">
							<uni-grid-item v-for="(item,index) in icon.slice(0,8)" :key="index">
								<navigator url="LegalexpertiseIcon/LegalexpertiseIcon" style="height: 100%;">
									<view
										style="height: 100%; display: flex; justify-content: center; align-items: center; flex-direction: column;">
										<image :src="$u.a+item.imgUrl" style="width: 80rpx; height: 80rpx;" mode="">
										</image>
										<view>{{item.name}}</view>
									</view>
								</navigator>
							</uni-grid-item>
						</uni-grid>
					</swiper-item>
					<swiper-item>
						<uni-grid :column="4" :showBorder="false">
							<uni-grid-item v-for="(item,index) in icon.slice(8,16)" :key="index">
								<navigator url="LegalexpertiseIcon/LegalexpertiseIcon" style="height: 100%;">
									<view
										style="height: 100%; display: flex; justify-content: center; align-items: center; flex-direction: column;">
										<image :src="$u.a+item.imgUrl" style="width: 80rpx; height: 80rpx;" mode="">
										</image>
										<view>{{item.name}}</view>
									</view>
								</navigator>
							</uni-grid-item>
						</uni-grid>
					</swiper-item>
				</swiper>
			</view>
		</uni-section>

		<uni-section title="我的咨询" sub-title="" type="line">
			<navigator url="LegalexpertiseGuidance/LegalexpertiseGuidance" style="height: 100%;">
				<image style="border-radius: 20rpx;" src="../../static/lawyer/myLewyer.jpeg" mode=""></image>
			</navigator>
		</uni-section>

		<view style="height: 50rpx;"></view>
		<uni-section title="优选律师" sub-title="" type="line">
			<view v-for="(item,index) in list" :key="index">
				<uni-card>
					<view style="display: flex;">
						<view>
							<image :src="$u.a+item.avatarUrl"
								style="width: 320rpx; height: 320rpx; margin-right: 20rpx;" mode=""></image>
						</view>
						<view>
							<view style="font-weight: bold;">{{item.name}}</view>
							<view>从业年限:{{item.workStartAt}}年</view>
							<view>咨询人数:{{item.serviceTimes}}人</view>
							<view>法律专长:{{item.legalExpertiseName}}</view>
							<view>好评率:{{item.favorableRate}}%</view>
							<navigator :url="`LegalexpertiseDetail/LegalexpertiseDetail?id=${item.id}`"
								style="height: 100%;">
								<button type="primary" size="mini">咨询</button>
							</navigator>
						</view>
					</view>
				</uni-card>
			</view>
		</uni-section>
		<navigator url="LegalexpertiseList/LegalexpertiseList"><button type="primary">查看更多</button></navigator>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				sp: [],
				icon: [],
				list: []
			}
		},
		methods: {
			confirm(e) {
				uni.navigateTo({
					url: '/pages/four/LegalexpertiseLawyerList/LegalexpertiseLawyerList?id=' + e.value
				})
			}
		},
		onLoad() {
			this.$r.h(`/prod-api/api/lawyer-consultation/ad-banner/list`).then(res => {
				this.sp = res.data
			})

			this.$r.h(`/prod-api/api/lawyer-consultation/legal-expertise/list`).then(res => {
				this.icon = res.rows.sort(function(a, b) {
					return b.sort - a.sort
				})

			})

			this.$r.h(`/prod-api/api/lawyer-consultation/lawyer/list-top10`).then(res => {
				this.list = res.data
				let date = new Date()
				for (let s of this.list) {
					s.workStartAt = parseInt(date.getFullYear()) - parseInt(s.workStartAt.slice(0, 4))
				}
			})
		}
	}
</script>

<style>

</style>