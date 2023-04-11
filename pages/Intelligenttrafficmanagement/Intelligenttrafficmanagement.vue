<template>
	<view>
		<uni-section title="预约检车" sub-title="" type="line">
			1.在审车之前，确保已经处理好所有车辆的违章，否则检查进度将受到影响。不仅无法完成车辆年检，而且车主将不得不花费时间排队处理违章。希望大家在审车之前先检查自己的车辆是否有违章，然后再审车。
		</uni-section>
		<navigator url="carmssage/carmssage"><button type="primary">车辆管理</button></navigator>
		<navigator url="carVehicle/carVehicle"><button type="primary">立即预约</button></navigator>
		<navigator url="Myappointment/Myappointment"><button type="primary">我的预约</button></navigator>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		methods: {

		},
		onLoad() {

		}
	}
</script>

<style>

</style>