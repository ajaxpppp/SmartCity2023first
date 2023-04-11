<template>
	<view>
		<uni-section title="添加车辆" sub-title="" type="line">
			<uni-forms ref="form" style="margin: 50rpx;">
				<uni-forms-item label="车牌号" name="">
					<uni-easyinput v-model="plateNo" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="车架号">
					<uni-easyinput v-model="engineNo" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="车辆类型" name="">
					<uni-easyinput v-model="type" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="公里数">
					<uni-easyinput v-model="gl" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="手机号">
					<uni-easyinput v-model="phone" placeholder="" />
				</uni-forms-item>
				<button type="primary" @click="change">添加</button>
			</uni-forms>
		</uni-section>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				"engineNo": "1212XS123113",
				"plateNo": "辽 B666666",
				"type": "小型汽车",
				gl: "10",
				phone: "17722221111",
			}
		},
		methods: {
			change() {
				this.$r.h(`/prod-api/api/traffic/car`, 'post', {
					"engineNo": this.engineNo,
					"plateNo": this.plateNo,
					"type": this.type,
				}).then(res => {
					uni.showToast({
						title: res.msg
					});
				})
			}
		}
	}
</script>

<style>

</style>