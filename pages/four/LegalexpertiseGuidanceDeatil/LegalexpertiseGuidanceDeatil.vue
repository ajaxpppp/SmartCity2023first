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
						<view>从业年限:{{item.workStartAt}}</view>
						<view>咨询人数:{{item.serviceTimes}}人</view>
						<view>法律专长:{{item.legalExpertiseName}}</view>
						<view>好评率:{{item.favorableRate}}%</view>
					</view>
				</view>
			</uni-card>
		</uni-section>

		<uni-section title="问题信息" sub-title="" type="line">
			<uni-card>
				<view>
					<view>
						<image :src="$u.a+`/prod-api`+item.imageUrls"
							style="width: 100%; height: 320rpx; margin-right: 20rpx;" mode="">
						</image>
					</view>
					<view>
						<view>受理状态:{{item.state==1?"已处理":"未处理"}}</view>
						<view>问题类型:{{item.legalExpertiseName}}</view>
						<view>问题描述:{{item.content}}</view>
						<view>联系电话:{{item.phone}}</view>
					</view>
				</view>
				<navigator :url="`../LegalexpertiseGuidanceCommit/LegalexpertiseGuidanceCommit?id=${item.id}`"><button
						v-if="item.state==1" type="primary">评价</button></navigator>
			</uni-card>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				item: []
			}
		},
		methods: {

		},
		onLoad(e) {
			this.item = JSON.parse(e.id)
			let date = new Date()
			this.item.workStartAt = parseInt(date.getFullYear()) - parseInt(this.item.workStartAt.slice(0, 4))
		}
	}
</script>

<style>

</style>