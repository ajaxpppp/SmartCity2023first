<template>
	<view>
		<swiper style="height: 100vh;" :indicator-dots="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,index) in sp" :key="index">
				<image style="height: 100vh;" :src="item" mode=""></image>
				<button v-if="index==sp.length-1" @click="duan" type="primary"
					style="position: fixed; right: 0rpx; top: 0rpx;" plain="">端口设置</button>
				<button v-if="index==sp.length-1" @click="toindex" type="primary"
					style="position: fixed; left: 30%; bottom: 50rpx;">进入主页</button>
			</swiper-item>
		</swiper>

		<uni-popup ref="popup">
			<uni-popup-dialog @confirm="shen">
				<uni-forms ref="form">
					<uni-forms-item label="IP地址" name="">
						<uni-easyinput v-model="ip" placeholder="" />
					</uni-forms-item>
					<uni-forms-item label="端口" name="">
						<uni-easyinput v-model="port" placeholder="" />
					</uni-forms-item>
				</uni-forms>
			</uni-popup-dialog>
		</uni-popup>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				ip: uni.getStorageSync("ip") || "124.93.196.45",
				port: uni.getStorageSync("port") || "10001",

				sp: ['/static/bt/smartcity5.jpg',
					'/static/bt/smartcity4.jpg',
					'/static/bt/smartcity3.jpg',
					'/static/bt/smartcity2.jpg',
					'/static/bt/smartcity1.jpg'
				]
			}
		},
		methods: {
			duan() {
				this.$refs.popup.open()
			},
			shen() {
				uni.setStorageSync("ip", this.ip)
				uni.setStorageSync("port", this.port)
				uni.setStorageSync("url", `http://${this.ip}:${this.port}/`)
				this.$r.geturl()
				this.$u.a = `http://${this.ip}:${this.port}/`
				uni.showToast({
					title: '修改成功',

				});
			},
			toindex() {
				uni.reLaunch({
					url: '/pages/five/login/login',
					success: () => {
						uni.setStorageSync("key", true)
					}
				})
			}
		},
		onLoad() {
			if (uni.getStorageSync("key") == true) {
				uni.reLaunch({
					url: '/pages/five/login/login'

				})
			}
		}
	}
</script>

<style>

</style>