<template>
	<view>
		<uni-section title="成功预约的车辆信息" sub-title="" type="line">
			<uni-list v-for="(item,index) in list" :key="index">
				<uni-list-item :title="`车牌号:${item.plateNo}\n预约时间:${item.aptTime}\n预约检车地点:${item.addressId}`"
					note=""></uni-list-item>
			</uni-list>
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
			this.$r.h(`/prod-api/api/traffic/checkCar/apply/list`).then(res => {
				this.list = res.rows
				for (let s of this.list) {
					this.$r.h(`/prod-api/api/traffic/checkCar/place/${s.addressId}`).then(res => {
						s.addressId = res.data.address
					})
				}
			})
		}
	}
</script>

<style>

</style>