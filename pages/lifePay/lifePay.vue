<template>
	<view>
		<navigator url="lifePayList/lifePayList">
			<view style=" text-align: right; font-size: 50rpx;">交费记录
			</view>
		</navigator>

		<uni-section title=" 运营商" sub-title="" type="line">
			<radio-group style="padding: 50rpx;">
				<view style="display: flex;">
					<view style="padding-left: 25rpx;">中国移动<radio v-model="meth.yidong" @click="methodssss('中国移动')">
						</radio>
					</view>
					<view style="padding-left: 25rpx;">中国联通<radio v-model="meth.liantong" @click="methodssss('中国联通')">
						</radio>
					</view>
					<view style="padding-left: 25rpx;">中国电信<radio v-model="meth.dianxin" @click="methodssss('中国电信')">
						</radio>
					</view>
				</view>

			</radio-group>

			<view>
				<uni-forms-item label="手机号">
					<uni-easyinput v-model="phonenumber"></uni-easyinput>
				</uni-forms-item>
				<button type="primary" @click="chaxxun">查询</button>
			</view>
		</uni-section>

		<view>
			<view style="font-size: 40rpx; padding: 20rpx;">常用手机号</view>
			<view v-for="item in list" style=" margin: 25rpx;">
				<view>运营商名称:中国移动</view>
				<view>手机号:{{item.phonenumber}}</view>
				<view>添加时间:{{item.rechargeTime}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				meth: {
					yidong: '',
					liantong: '',
					dianxin: ''
				},
				phonenumber: '13800000000',
				operator: '',
				list: []
			}
		},
		methods: {

			// 13800000000
			chaxxun() {
				this.$r.h(`/prod-api/api/living/phone?operator=${this.operator}&phonenumber=${this.phonenumber}`).then(
					res => {
						if (res.code == 200) {
							uni.navigateTo({
								url: `/pages/lifePay/lifePayPayment/lifePayPayment?id=${this.phonenumber}`
							})
						} else {
							uni.showToast({
								title: '运营商或手机号错误'
							})
						}
					})
			},
			methodssss(str) {
				this.operator = str
			},
		},
		onLoad() {
			this.$r.h(`/prod-api/api/living/phone/record/list`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>