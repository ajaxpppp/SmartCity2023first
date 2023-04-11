<template>
	<view>
		<uni-section title="添加车辆" sub-title="" type="line">
			<uni-forms ref="form" style="margin: 50rpx;">
				<uni-forms-item label="录入的车辆" name="">
					<radio-group>
						<label v-for="(item,index) in cars.slice(0,3)" :key="index">
							<radio @click="to(item.id,item.userId)" /><text>{{item.type}}</text>
						</label>
					</radio-group>
				</uni-forms-item>
				<uni-forms-item label="选择时间">
					<uni-datetime-picker v-model="data"></uni-datetime-picker>
				</uni-forms-item>
				<uni-forms-item label="检车地点" name="">
					<uni-data-select :localdata="localdata" v-model="value"></uni-data-select>
				</uni-forms-item>
				<button type="primary" @click="change">预约</button>
			</uni-forms>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cars: [],
				localdata: [],
				value: 0,
				data: "",
				cid: "",
				uid: ''
			}
		},
		methods: {
			to(e, v) {
				this.cid = e
				this.uid = v
			},
			change() {
				this.$r.h(`/prod-api/api/traffic/checkCar/apply`, "post", {
					"userId": this.uid,
					"carId": this.cid,
					"aptTime": this.data,
					"addressId": this.value
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: "预约成功"
						});
						setTimeout(() => {
							uni.navigateTo({
								url: "/pages/Intelligenttrafficmanagement/Myappointment/Myappointment"
							})
						}, 1500)
					} else {
						uni.showToast({
							title: res.msg
						});
					}
				})
			}
		},
		onLoad() {
			this.$r.h(`/prod-api/api/traffic/car/list`).then(res => {
				this.cars = res.rows.sort(function(a, b) {
					return b.id > a.id ? 1 : -1
				})
			})

			this.$r.h(`/prod-api/api/traffic/checkCar/place/list`).then(res => {
				for (let s of res.rows) {
					let text
					let value
					this.localdata.push({
						text: s.address,
						value: s.id
					})
				}
			})
		}
	}
</script>

<style>

</style>