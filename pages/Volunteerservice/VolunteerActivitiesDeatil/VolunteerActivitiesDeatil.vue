<template>
	<view>
		<uni-section title="活动详情信息" sub-title="" type="line">

			<uni-list>
				<uni-list-item title="" note="">
					<template v-slot:body>
						<view style="display: flex;">
							<view>
								<view style="font-size: 55rpx; font-weight: bold;">{{item.title}}</view>
								<rich-text :nodes="`活动简介:`+item.detail"></rich-text>
								<view style="text-align: right; margin-top: 50rpx;">
									<view>活动开始时间:{{item.startAt}}</view>
									<view>人员要求:{{item.requireText}}</view>
									<view>承办单位:{{item.undertaker}}</view>
									<view>工作内容:处理场内秩序</view>
								</view>
							</view>
						</view>
					</template>
				</uni-list-item>
			</uni-list>

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
			this.$r.h(`/prod-api/api/volunteer-service/activity/` + e.id).then(res => {
				this.item = res.data
			})
		}
	}
</script>

<style>

</style>