<template>
	<view>
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,index) in list.imageUrlList" :key="index">
				<image :src="$u.a+item" mode=""></image>
			</swiper-item>
		</swiper>

		<uni-section title="驿站详情" sub-title="" type="line" style="margin: 50rpx;">
			<view>驿站地址:{{list.address}}</view>
			<view>联系电话:{{list.phone}}</view>
			<view>入住时间段:{{list.workTime}}</view>
			<view>剩余男床位数:{{list.bedsCountBoy}}间</view>
			<view>剩余女床位数:{{list.bedsCountGirl}}间</view>
			<view>周边配套:{{list.surroundingFacilities}}</view>
			<view>特色服务:{{list.specialService}}</view>
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
			this.$r.h(`/prod-api/api/youth-inn/youth-inn/` + e.id).then(res => {
				this.list = res.data
			})
		}
	}
</script>

<style>

</style>
