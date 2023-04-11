<template>
	<view>
		<view style="text-align: right; font-size: 50rpx;" @click="listto">常用手机号</view>
		<view style="text-align: center;">手机号:{{phonenumber}}</view>
		<view>
			<uni-grid>
				<uni-grid-item v-for="item in money">
					<image @click="mmmm(item)" src="../../../static/bt/c1.png" style="width: 100%;" mode=""></image>
					<text style="text-align: center;">{{item}}元</text>
				</uni-grid-item>
			</uni-grid>
			<button type="primary" @click="tinaqi">去支付</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				phonenumber: "",
				money: [50, 100, 200],
				zhifu: {
					"paymentType": "电子支付",
					"phonenumber": 0,
					"rechargeAmount": 50,
					"ruleId": 1,
					"type": "2"
				}

			}
		},
		methods: {
			listto() {
				uni.showToast({
					title: "手机号13800000000添加成功"
				})
			},
			mmmm(num) {
				this.zhifu.rechargeAmount = num
				this.zhifu.phonenumber = this.phonenumber
			},
			tinaqi() {
				this.$r.h(`/prod-api/api/living/phone/recharge`, 'post', {
					"paymentType": "电子支付",
					"phonenumber": this.zhifu.phonenumber,
					"rechargeAmount": this.zhifu.rechargeAmount,
					"ruleId": 1,
					"type": "1"
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: `充值金额` + this.zhifu.rechargeAmount + `元`,
						})
					} else {
						uni.showToast({
							title: "请输入手机号",
							icon: 'error'
						})
					}
				})
			},
		},
		onLoad(e) {
			this.phonenumber = e.id
		}
	}
</script>

<style>

</style>