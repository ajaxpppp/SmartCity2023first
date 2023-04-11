<template>
	<view>
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,index) in sp" :key="index">
				<navigator :url="`ActiveDetail/ActiveDetail?id=${item.id}`" style="height: 100%;">
					<image :src="$u.a+item.advImg" style="width: 100%; height: 100%;" mode=""></image>
				</navigator>
			</swiper-item>
		</swiper>

		<uni-section title="活动列表" sub-title="" type="line">
			<uni-row>
				<uni-col :span="24/text.length" v-for="(item,index) in text" :key="index">
					<view @click="textc(item.id)" style="text-align: center;" :style="id==item.id?'color:blue':''">
						{{item.name}}
					</view>
				</uni-col>
			</uni-row>

			<view v-for="(item,index) in list" :key="index">
				<uni-card>
					<navigator :url="`ActiveDetail/ActiveDetail?id=${item.id}`" style="height: 100%;">
						<view style="display: flex;">
							<view>
								<image :src="$u.a+item.imgUrl"
									style="width: 320rpx; height: 320rpx; margin-right: 20rpx;" mode=""></image>
							</view>
							<view>

								<view style="font-weight: bold;">{{item.name}}</view>
								<view>报名人数:{{item.signupNum}}</view>
								<view>点赞数:{{item.likeNum}}</view>
								<button type="primary" size="mini" @click.stop="addactive(item.id)">报名</button>
							</view>
						</view>
					</navigator>
				</uni-card>
			</view>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				sp: [],
				list: [],
				text: [],
				id: 1,
			}
		},
		methods: {
			addactive(e) {
				this.$r.h(`/prod-api/api/activity/signup`, 'post', {
					"activityId": e
				}).then(res => {
					uni.showToast({
						title: res.msg
					});
				})
			},
			textc(e) {
				this.id = e
				this.$r.h(`/prod-api/api/activity/activity/list?categoryId=${e}`).then(res => {
					this.list = res.rows
				})
			}
		},
		onLoad() {
			this.textc(this.id)
			this.$r.h(`/prod-api/api/activity/rotation/list`).then(res => {
				this.sp = res.rows
			})

			this.$r.h(`/prod-api/api/activity/category/list`).then(res => {
				this.text = res.data
			})
		}
	}
</script>

<style>

</style>
