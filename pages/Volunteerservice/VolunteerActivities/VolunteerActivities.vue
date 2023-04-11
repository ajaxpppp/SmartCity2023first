<template>
	<view>
		<uni-search-bar @confirm="confirm" @input="" placeholder="搜索" />

		<uni-section title="活动列表" sub-title="" type="line">
			<view v-for="(item,index) in list" :key="index">
				<uni-list>
					<uni-list-item title="" note="">
						<template v-slot:body>
							<navigator :url="`../VolunteerActivitiesDeatil/VolunteerActivitiesDeatil?id=${item.id}`">
								<view style="display: flex;">
									<view>
										<view style="font-size: 35rpx; font-weight: bold;">{{item.title}}</view>
										<view>承办单位:{{item.undertaker}}</view>
										<view>活动开始时间:{{item.startAt}}</view>
										<view>人员要求:{{item.requireText}}</view>
									</view>
									<view> <button type="primary" @click.stop="bao(item.id)">报名</button></view>
								</view>
							</navigator>
						</template>

					</uni-list-item>
				</uni-list>
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
			confirm(e) {
				uni.showToast({
					title: '刷新成功'
				});
			},
			bao(e) {
				this.$r.h(`/prod-api/api/volunteer-service/register`, 'post', {
					"activityId": e,
					"newState": true
				}).then(res => {
					uni.showToast({
						title: '报名成功'
					});
				})
			}
		},
		onLoad() {
			this.$r.h(`/prod-api/api/volunteer-service/activity/list`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>