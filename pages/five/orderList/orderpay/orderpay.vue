<template>
	<view>
		<uni-section title="支付订单" sub-title="" type="line">
			<uni-forms ref="form" style="margin: 100rpx;">
				<uni-forms-item label="订单号" name="">
					<uni-easyinput v-model="item.orderNum" :disabled="true" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="支付金额" name="">
					<uni-easyinput v-model="item.price" :disabled="true" placeholder="" />
				</uni-forms-item>
				<button type="primary" style="margin: 50rpx;" @click="commit">支付订单</button>
			</uni-forms>
		</uni-section>

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
			commit() {
				this.$r.h(`/prod-api/api/bus/pay`, 'post', {
					"orderNum": this.item.orderNum,
					"paymentType": "电子支付"
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: "支付成功",
						});
						setTimeout(() => {
							uni.navigateTo({
								url: "/pages/five/orderList/orderList",
							});
						}, 2000)
					}
				})
			}
		},
		onLoad(e) {
			this.item = JSON.parse(e.id)
		}
	}
</script>

<style>

</style>