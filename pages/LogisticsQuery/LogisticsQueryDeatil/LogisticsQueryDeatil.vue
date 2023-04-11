<template>
	<view>
		<image :src="$u.a+item.imgUrl" mode=""></image>
		<uni-section title="公司简介" sub-title="" type="line">
			<view>{{item.introduce}}</view>
		</uni-section>
		<view style="text-align: right; margin-top: 50rpx;">
			<view>运输方式:{{item.shippingMethod}}</view>
			<view>运费介绍:200</view>
		</view>

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
			this.$r.h(`/prod-api/api/logistics-inquiry/logistics_company/` + e.id).then(res => {
				this.item = res.data
			})
		}
	}
</script>

<style>

</style>