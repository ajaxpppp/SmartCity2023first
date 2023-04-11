<template>
	<view>
		<uni-search-bar @confirm="confirm" @input="" placeholder="请输入物流单号" />

		<view>
			<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
				<swiper-item v-for="(item,index) in sp" :key="index">
					<image @click="imgto(item.id)" :src="$u.a+item.imgUrl" style="height: 100%;" mode=""></image>
				</swiper-item>
			</swiper>
		</view>


		<uni-section title="物流公司推荐" sub-title="" type="line">
			<uni-grid :column="4" :showBorder="false">
				<uni-grid-item v-for="(item,index) in icon.slice(0,12)" :key="index">
					<navigator :url="`LogisticsQueryDeatil/LogisticsQueryDeatil?id=${item.id}`">
						<view class="imgs" @click="tomore(item.serviceName)">
							<image style="width: 80rpx; height: 80rpx;" :src="$u.a+item.imgUrl" mode=""></image>
							<view>{{item.name}}</view>
						</view>
					</navigator>
				</uni-grid-item>
			</uni-grid>
		</uni-section>

		<uni-section title="其他物流公司推荐" sub-title="" type="line">
			<view v-for="(item,index) in icon" :key="index">
				<uni-list>
					<uni-list-item :title="`${item.name}`" note="">
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
				sp: [],
				icon: []
			}
		},
		methods: {
			confirm() {
				uni.navigateTo({
					url: '/pages/LogisticsQuery/LogisticsWaybillDeatil/LogisticsWaybillDeatil'
				});
			}
		},
		onLoad() {
			this.$r.h(`/prod-api/api/logistics-inquiry/ad-banner/list`).then(res => {
				this.sp = res.data
			})

			this.$r.h(`/prod-api/api/logistics-inquiry/logistics_company/list`).then(res => {
				this.icon = res.data
			})
		}
	}
</script>

<style>

</style>