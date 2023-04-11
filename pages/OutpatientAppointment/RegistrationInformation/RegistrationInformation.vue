<template>
	<view>
		<uni-section title="预约挂号信息" sub-title="" type="line">
			<uni-forms ref="form" style="padding: 100rpx;">

				<uni-forms-item label="预约科室">
					<uni-easyinput v-model="ke" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="门诊类型" name="">
					<uni-easyinput v-model="type" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="患者姓名" name="">
					<uni-easyinput v-model="user.userName" placeholder="请输入姓名" />
				</uni-forms-item>
				<uni-forms-item label="金额" name="">
					<uni-easyinput v-model="money" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="预约时间">
					<uni-easyinput v-model="reserveTime" placeholder="" />
				</uni-forms-item>
				<button type="primary" @click="change">预约成功</button>
			</uni-forms>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id: "",
				"categoryId": 0,
				"money": 50,
				"patientName": "",
				"reserveTime": this.$r.getDate(),
				"type": 1,
				ke: "",
				type: "普通",
				user: ""
			}
		},
		methods: {
			change() {
				this.$r.h(`/prod-api/api/hospital`, 'post', {
					"categoryId": this.id,
					"money": this.money,
					"patientName": this.patientName,
					"reserveTime": this.reserveTime,
					"type": 1
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: res.msg
						});
						setTimeout(() => {
							uni.reLaunch({
								url: '/pages/OutpatientAppointment/OutpatientAppointment'
							})
						}, 2000)
					} else {
						uni.showToast({
							title: res.msg
						});
					}
				})
			}
		},
		onLoad(e) {
			this.id = e.id
			this.ke = e.name
			this.user = uni.getStorageSync("user");
		}
	}
</script>

<style>

</style>
