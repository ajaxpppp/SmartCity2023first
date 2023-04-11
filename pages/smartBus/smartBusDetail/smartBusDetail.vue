<template>
	<view>
		<view v-if="temp==0">
			<uni-card>
				<view>起点:{{item.first}}</view>
				<view>票价:{{item.price}}元</view>
				<view>里程:{{item.mileage}}公里</view>
			</uni-card>
			<button type="primary" @click="pre">返回上级目录</button>
			<button type="primary" @click="next">下一步</button>
		</view>
		<view v-if="temp==1">
			<uni-datetime-picker v-model="data" style="margin: 50rpx; width: 650rpx;"></uni-datetime-picker>
			<button type="primary" @click="pre">返回上级目录</button>
			<button type="primary" @click="next">下一步</button>
		</view>
		<view v-if="temp==2">
			<uni-forms ref="form" style="padding: 100rpx;">
				<uni-forms-item label="乘客姓名">
					<uni-easyinput v-model="name" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="手机号码" name="">
					<uni-easyinput v-model="phone" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="上车地点">
					<uni-easyinput v-model="start" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="下车地点">
					<uni-easyinput v-model="end" placeholder="" />
				</uni-forms-item>
			</uni-forms>
			<button type="primary" @click="pre">返回上级目录</button>
			<button type="primary" @click="next">下一步</button>
		</view>
		<view v-if="temp==3">
			<uni-forms ref="form" style="padding: 100rpx;">
				<uni-forms-item label="乘客姓名">
					<uni-easyinput v-model="name" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="手机号码" name="">
					<uni-easyinput v-model="phone" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="上车地点">
					<uni-easyinput v-model="start" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="下车地点">
					<uni-easyinput v-model="end" placeholder="" />
				</uni-forms-item>
				<uni-datetime-picker v-model="data"></uni-datetime-picker>
			</uni-forms>
			<button type="primary" @click="pre">返回上级目录</button>
			<button type="primary" @click="sumbit">提交订单</button>
		</view>




	</view>
</template>

<script>
	export default {
		data() {
			return {
				temp: 0,
				item: [],
				data: "",
				name: "",
				phone: "",
				"start": "",
				"end": "",
				"price": "8",
				"path": "",
				"status": 1
			}
		},
		methods: {
			sumbit() {
				if (this.temp == 3) {
					this.$r.h(`/prod-api/api/bus/order`, 'post', {
						"start": this.start,
						"end": this.end,
						"price": "8",
						"path": "一号线",
						"status": 1
					}).then(res => {
						if (res.code == 200) {
							uni.navigateBack({
								delta: 1
							});
						}
					})
				}
			},
			next() {
				this.temp += 1

			},
			pre() {
				this.temp -= 1
				if (this.temp < 0) {
					uni.navigateBack({
						delta: 1
					});
				}

			}
		},
		onLoad(e) {
			this.$r.h(`/prod-api/api/bus/line/${e.id}`).then(res => {
				this.item = res.data
			})
		}
	}
</script>

<style>

</style>