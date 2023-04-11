<template>
	<view>
		<view>
			<image :src="$u.a+item.pic" mode=""></image>
			<view>房源名称:{{item.sourceName}}</view>
			<view>建筑面积:{{item.areaSize}}</view>
			<view>房源单价:{{item.price}}</view>
			<view>房源类型:二手</view>
			<view>房源介绍:{{item.description}}</view>
			<navigator url="../tohuntahouse"><button type="primary" style="margin: 50rpx;">主页 </button></navigator>
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
			this.$r.h(`/prod-api/api/house/housing/` + e.id).then(res => {
				this.item = res.data
			})
		}
	}
</script>

<style>

</style>
