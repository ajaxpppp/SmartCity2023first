<template>
	<view>
		<uni-segmented-control :current="current" :values="item" @clickItem="clickItem"></uni-segmented-control>
		<view class="content">
			<view v-show="current === 0">
				<view v-for="(item,index) in list" :key="index">
					<uni-list>
						<uni-list-item title="" note="">
							<template v-slot:body>
								<navigator
									:url="`../VolunteerActivitiesDeatil/VolunteerActivitiesDeatil?id=${item.id}`">
									<view style="display: flex;">
										<view>
											<view style="font-size: 35rpx; font-weight: bold;">{{item.title}}</view>
											<view>承办单位:{{item.undertaker}}</view>
											<view>活动开始时间:{{item.startAt}}</view>
											<view>人员要求:{{item.requireText}}</view>
										</view>
									</view>
								</navigator>
							</template>
						</uni-list-item>
					</uni-list>
				</view>
			</view>
			<view v-show="current === 1">
				<view v-for="(item,index) in list" :key="index">
					<uni-list>
						<uni-list-item title="" note="">
							<template v-slot:body>
								<navigator
									:url="`../VolunteerActivitiesDeatil/VolunteerActivitiesDeatil?id=${item.id}`">
									<view style="display: flex;">
										<view>
											<view style="font-size: 35rpx; font-weight: bold;">{{item.title}}</view>
											<view>承办单位:{{item.undertaker}}</view>
											<view>活动开始时间:{{item.startAt}}</view>
											<view>人员要求:{{item.requireText}}</view>
											<button type="primary" size="mini" @click.stop="bao(item.id)">取消报名</button>
										</view>
									</view>
								</navigator>
							</template>

						</uni-list-item>
					</uni-list>
				</view>
			</view>
			<view v-show="current === 2">
				<view v-for="(item,index) in list.slice(0,3)" :key="index">
					<uni-list>
						<uni-list-item title="" note="">
							<template v-slot:body>
								<navigator
									:url="`../VolunteerActivitiesDeatil/VolunteerActivitiesDeatil?id=${item.id}`">
									<view style="display: flex;">
										<view>
											<view style="font-size: 35rpx; font-weight: bold;">{{item.title}}</view>
											<view>承办单位:{{item.undertaker}}</view>
											<view>活动开始时间:{{item.startAt}}</view>
											<view>人员要求:{{item.requireText}}</view>
										</view>
									</view>
								</navigator>
							</template>

						</uni-list-item>
					</uni-list>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				current: 0,
				list: [],
				item: ['已完成', '已报名', '已取消']
			}
		},
		methods: {
			clickItem(e) {
				this.current = e.currentIndex
			},
			bao(e) {
				this.$r.h(`/prod-api/api/volunteer-service/register`, 'post', {
					"activityId": e,
					"newState": false
				}).then(res => {
					uni.showToast({
						title: '已取消'
					});
					console.log("res: " + JSON.stringify(res));
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