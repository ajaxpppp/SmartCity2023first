<template>
	<view>
		<uni-search-bar @confirm="confirm" placeholder="搜索外卖" @input="" />
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,index) in sp" :key="index">
				<image :src="$u.a+item.advImg" style="width: 100%; height: 100%;"></image>
			</swiper-item>
		</swiper>

		<uni-section title="美食分类功能入口" sub-title="" type="line">
			<uni-grid :column="5" :showBorder="false">
				<uni-grid-item v-for="(item,index) in icon.slice(0,9)" :key="index">
					<navigator :url="`TakeOutorderList/TakeOutorderList?id=${item.id}`" style="height: 100%;">
						<view class="imgs">
							<image :src="$u.a+item.imgUrl" style="width: 80rpx; height: 80rpx; border-radius: 50%;"
								mode="">
							</image>
							<view>{{item.themeName}}</view>
						</view>
					</navigator>

				</uni-grid-item>
			</uni-grid>
		</uni-section>

		<uni-section title="附件商家模块" sub-title="" type="line">
			<view v-for="(item,index) in list" :key="index">
				<uni-card>
					<navigator :url="`TakeOutorderDetail/TakeOutorderDetail?id=${item.id}`" style="height: 100%;">
						<view style="display: flex;">
							<view>
								<image :src="$u.a+item.imgUrl"
									style="width: 320rpx; height: 320rpx; margin-right: 20rpx;" mode=""></image>
							</view>
							<view>
								<view style="font-weight: bold;">{{item.name}}</view>
								<view style="font-size: 1rpx; display: flex;">评分:<uni-rate
										:value="item.score"></uni-rate></view>
								<view>月销量:{{item.saleQuantity}}</view>
								<view>到店所需时间:{{item.deliveryTime}}</view>
								<view>人均消费:{{item.distance}}</view>
							</view>
						</view>
					</navigator>
				</uni-card>
			</view>
		</uni-section>

		<view
			style="position: fixed; bottom: 0; background-color: #ffffff; height: 120rpx; width: 100%; margin: 0 auto;">
			<uni-grid :column="3" :showBorder="false">
				<uni-grid-item>
					<navigator url="VolunteerActivities/VolunteerActivities">
						<view class="imgs">
							<image src="../../static/volun/bus2.png" style=" width: 80rpx ; height: 80rpx;" mode="">
							</image>
							<view style="color: red;">首页</view>
						</view>
					</navigator>
				</uni-grid-item>

				<uni-grid-item>
					<navigator url="Deliveryorder/Deliveryorder">
						<view class="imgs">
							<image src="../../static/volun/bus2.png" style="width: 80rpx ; height: 80rpx;" mode="">
							</image>
							<view>订单</view>
						</view>
					</navigator>
				</uni-grid-item>

				<uni-grid-item>
					<navigator url="Mytakeout/Mytakeout">
						<view class="imgs">
							<image src="../../static/volun/bus2.png" style="width: 80rpx ; height: 80rpx;" mode="">
							</image>
							<view>我的</view>
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
				sp: [],
				icon: [],
				list: []
			}
		},
		methods: {
			confirm(e) {
				uni.navigateTo({
					url: '/pages/TakeOutorder/TakeSearch/TakeSearch?name=' + e.value
				})
			}
		},
		onLoad() {
			this.$r.h(`/prod-api/api/takeout/rotation/list`).then(res => {
				this.sp = res.rows

			})

			this.$r.h(`/prod-api/api/takeout/theme/list`).then(res => {
				this.icon = res.data

			})

			this.$r.h(`/prod-api/api/takeout/seller/near`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>