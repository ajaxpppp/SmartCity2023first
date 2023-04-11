<template>
	<view>
		<view v-for="item in list" style="margin: 50rpx;">
			<view>手机号:{{item.phonenumber}}</view>
			<view>添加时间:{{item.rechargeTime}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: []
			}
		},
		methods: {},
		onLoad() {
			this.$r.h(`/prod-api/api/living/phone/record/list`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>