<template>
	<view>
		<uni-forms ref="form" style="margin: 50rpx;">
			<uni-forms-item label="快递单号" name="">
				<uni-easyinput v-model="infoNo" placeholder="" />
			</uni-forms-item>
			<uni-forms-item label="投诉问题" name="">
				<textarea v-model="pwd" maxlength="150" style="width: 100%; border: 1px solid;" placeholder="" />
				字数:{{pwd.length}}
			</uni-forms-item>
			<button type="primary" @click="login">确认</button>
		</uni-forms>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				"companyId": 7,
				"infoNo": "ST0000001",
				"questionType": "1",
				"description": "帮我看看这个快递到底是怎么回事，谢谢。",
				id: 0,
				pwd: ""
			}
		},
		methods: {
			login() {
				this.$r.h(`/prod-api/api/logistics-inquiry/logistics_complaint`, 'post', {
					"companyId": this.id,
					"infoNo": "ST0000001",
					"questionType": "1",
					"description": this.pwd
				}).then(res => {
					console.log("res: " + JSON.stringify(res));
					if (res.code == 200) {
						uni.reLaunch({
							url: "/pages/LogisticsQuery/Logisticscomplaints/Logisticscomplaints"
						})
					}
				})
			}
		}
	}
</script>

<style>

</style>