<template>
	<view>
		<view>
			<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
				<swiper-item v-for="(item,index) in sp" :key="index">
					<image @click="toimg(item.id)" :src="$u.a+item.imgUrl" style="height: 100%;" mode=""></image>
				</swiper-item>
			</swiper>
		</view>

		<uni-section title="新闻列表" sub-title="" type="line">
			<view v-for="(item,index) in list" :key="index">
				<uni-list>
					<uni-list-item title="" note="">
						<template v-slot:body>
							<navigator :url="`VolunteerActivitiesDeatil/VolunteerActivitiesDeatil?id=${item.id}`">
								<view style="display: flex;">
									<view>
										<image
											style="width: 320rpx; height: 220rpx; border-radius: 20rpx; margin-right: 20rpx;"
											:src="$u.a+item.imgUrl" mode=""></image>
									</view>
									<view>
										<view style="font-size: 35rpx; font-weight: bold;">{{item.title}}</view>
										<rich-text :nodes="item.summary?item.summary.slice(0,20)+'...':''"></rich-text>
										<view>发布时间:{{item.createTime}}</view>
									</view>
								</view>
							</navigator>
						</template>

					</uni-list-item>
				</uni-list>
			</view>
		</uni-section>

		<view
			style="position: fixed; bottom: 0; background-color: #ffffff; height: 120rpx; width: 100%; margin: 0 auto;">
			<uni-grid :column="2" :showBorder="false">
				<uni-grid-item>
					<navigator url="VolunteerActivities/VolunteerActivities">
						<view class="imgs">
							<image src="../../static/volun/bus2.png" style="width: 80rpx ; height: 80rpx;" mode="">
							</image>
							</image>
							<view>志愿活动</view>
						</view>
					</navigator>
				</uni-grid-item>

				<uni-grid-item>
					<navigator url="MyActivities/MyActivities">
						<view class="imgs">
							<image src="../../static/volun/bus2.png" style="width: 80rpx ; height: 80rpx;" mode="">
							</image>
							<view>我的活动</view>
						</view>
					</navigator>
				</uni-grid-item>
			</uni-grid>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [],
				sp: []
			}
		},
		methods: {

		},
		onLoad() {
			this.$r.h(`/prod-api/api/volunteer-service/ad-banner/list`).then(res => {
				this.sp = res.data
			})

			this.$r.h(`/prod-api/api/volunteer-service/news/list`).then(res => {
				this.list = res.rows.sort(function(a, b) {
					// return new Date(b.createTime).getTime()-new Date(a.createTime).getTime()
					return a.createTime > b.createTime ? -1 : 1
				})
			})
		}
	}
</script>

<style>

</style>