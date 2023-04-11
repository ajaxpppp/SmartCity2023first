<template>
	<view>
		<uni-section title="巴士列表" sub-title="" type="line">
			<uni-card v-for="(item,index) in list" :key="index">
				<navigator :url="`smartBusDetail/smartBusDetail?id=${item.id}`">
					<view>路线名称:{{item.name}}</view>
					<view>起终点:{{item.first}}</view>
					<view>运行时间:{{item.startTime}}~{{item.endTime}}</view>
					<view>票价:{{item.price}}元</view>
					<view>里程:{{item.mileage}}公里</view>
				</navigator>
			</uni-card>
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
		onLoad() {
			this.$r.h(`/prod-api/api/bus/line/list`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>