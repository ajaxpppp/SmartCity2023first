<template>
	<view>
		<uni-section title="就诊人卡片" sub-title="" type="line">
			<view v-for="(item,index) in list.slice(0,3)" :key="index">
				<uni-card>
					<navigator url="../administrativeortechnicaloffices/administrativeortechnicaloffices">
						<view style="text-align: right; font-size: 70rpx;">>></view>
					</navigator>
					<navigator url="../addoutpatientAppointment/addoutpatientAppointment" style="height: 100%;">
						<view style="display: flex;">
							<view>
								<view style="font-weight: bold;"></view>
								<view>姓名:{{item.name}}</view>
								<view>性别:{{item.sex}}</view>
								<view>身份证号:{{item.cardId}}</view>
								<view>出生日期:{{item.birthday}}</view>
								<view>手机号:{{item.tel}}</view>
							</view>
						</view>
					</navigator>
				</uni-card>
			</view>
			<uni-section title="新增就诊人" sub-title="" type="line">
				<uni-card>
					<navigator url="../addoutpatientAppointment/addoutpatientAppointment">
						<image style="height: 280rpx;" src="../../../static/haveanappointmentwithadocterphoto/add.jpeg"
							mode="">
					</navigator>
					</image>
				</uni-card>
			</uni-section>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [],
				user: uni.getStorageSync("user")
			}
		},
		methods: {

		},
		onShow() {
			this.$r.h(`/prod-api/api/hospital/patient`, 'post', {
				"address": "湖南省怀化市",
				"birthday": "2000-10-10",
				"cardId": this.user.idCard,
				"name": this.user.userName,
				"sex": this.user.sex == "0" ? "男" : "女",
				"tel": this.user.phonenumber
			}).then(res => {
				if (res.code == 200) {
					this.$r.h(`/prod-api/api/hospital/patient/list`).then(res => {
						this.list = res.rows.sort(function(a, b) {
							return b.createTime > a.createTime ? 1 : -1
						})
					})
				} else {
					uni.showToast({
						title: res.msg
					});
				}
			})
		}
	}
</script>

<style>

</style>
