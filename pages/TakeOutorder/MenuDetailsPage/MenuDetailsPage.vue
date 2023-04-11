<template>
	<view>
		<view>
			<view>
				<image :src="$u.a+item.imgUrl" style=" margin-right: 20rpx;" mode="">
				</image>
			</view>
			<view>
				<view style="font-weight: bold;">菜品名称:{{item.name}}</view>
				<view>月销量:{{item.saleQuantity}}</view>
				<view>菜品分类:西餐</view>
				<view>菜品详情:{{item.detail}}</view>
			</view>
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
			this.item = JSON.parse(e.id)
		}
	}
</script>

<style>

</style>