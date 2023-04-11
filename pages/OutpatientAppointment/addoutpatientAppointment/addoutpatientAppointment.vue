<template>
	<view>
		<uni-forms ref="form" style="padding: 100rpx;">
			<uni-forms-item label="姓名*" name="">
				<uni-easyinput v-model="name" placeholder="" />
			</uni-forms-item>
			<uni-forms-item label="性别*">
				<uni-data-checkbox :localdata="localdata" v-model="value"></uni-data-checkbox>
			</uni-forms-item>
			<uni-forms-item label="身份证号*">
				<uni-easyinput v-model="cardId" placeholder="" />
			</uni-forms-item>
			<uni-forms-item label="出生日期*">
				<uni-easyinput v-model="birthday" placeholder="" />
			</uni-forms-item>
			<uni-forms-item label="手机号*" name="">
				<uni-easyinput v-model="tel" placeholder="" />
			</uni-forms-item>
			<uni-forms-item label="地址">
				<uni-easyinput v-model="address" placeholder="" />
			</uni-forms-item>
			<button type="primary" @click="change">确定</button>
		</uni-forms>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				value: "0",
				localdata: [{
					text: "男",
					value: "0"
				}, {
					text: "女",
					value: "1"
				}],
				address: "",
				birthday: "",
				cardId: "",
				name: "",
				sex: "",
				tel: ""
			}
		},
		methods: {
			change() {
				this.$r.h(`/prod-api/api/hospital/patient`, 'post', {
					"address": this.address,
					"birthday": this.birthday,
					"cardId": this.cardId,
					"name": this.name,
					"sex": this.value,
					"tel": this.tel
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: res.msg
						});
						this.address = ""
						this.birthday = ""
						this.cardId = ""
						this.name = ""
						this.value = ""
						this.tel = ""
					} else {
						uni.showToast({
							title: "请注意格式"
						});
					}
				})
			}
		},
		onLoad() {

		}
	}
</script>

<style>

</style>
