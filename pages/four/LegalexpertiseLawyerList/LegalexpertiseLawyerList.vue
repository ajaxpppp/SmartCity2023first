<template>
	<view>
		<uni-section title="律师列表" sub-title="" type="line">
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
							<navigator :url="`../LegalexpertiseDetail/LegalexpertiseDetail?id=${item.id}`"
								style="height: 100%;">
								<button type="primary" size="mini">咨询</button>
							</navigator>
						</view>
					</view>
				</uni-card>
			</view>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: []
			}
		},
		methods: {

		},
		onLoad(e) {
			this.$r.h(`/prod-api/api/lawyer-consultation/lawyer/list?name=${e.id}`).then(res => {
				this.list = res.rows
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
