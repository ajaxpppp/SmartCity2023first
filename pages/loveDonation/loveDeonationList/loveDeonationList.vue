<template>
	<view>
		<uni-section title="公益列表" sub-title="" type="line">
			<view v-for="(item,index) in list" :key="index">
				<uni-card>
					<navigator :url="`../loveDonationDetail/loveDonationDetail?id=${JSON.stringify(item)}`"
						style="height: 100%;">
						<view style="display: flex;">
							<view>
								<image :src="$u.a+item.imgUrl"
									style="width: 320rpx; height: 320rpx; margin-right: 20rpx;" mode=""></image>
							</view>
							<view>
								<view style="font-weight: bold;">{{item.name}}</view>
								<view>发布组织:{{item.author}}</view>
								<view>发布人:刘零二</view>
								<view>已筹善款:{{item.moneyNow}}</view>
								<view>项目时间:{{item.activityAt}}</view>
								<view>捐赠人数:{{item.donateCount}}</view>
							</view>
						</view>
					</navigator>
				</uni-card>
			</view>

			<view>
				<uni-forms-item label="金额" name="" style="margin: 50rpx;">
					<uni-easyinput v-model="money" placeholder="请输入捐款金额" />
				</uni-forms-item>
				<button type="primary" @click="tohelp">我要捐助</button>
				<navigator url="../loveDonation"><button type="primary">分页</button></navigator>
			</view>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [],
				money: null,
			}
		},
		methods: {
			tohelp() {
				this.$r.h(`/prod-api/api/public-welfare/donate-record`, 'post', {
					"activityId": this.id,
					"donateMoney": this.money
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: res.msg + `捐款${this.money}元`
						});
						this.money = ""
					} else {
						uni.showToast({
							title: '捐款失败请检查'
						});
					}

				})
			}
		},
		onLoad(e) {
			this.id = e.id
			this.$r.h(`/prod-api/api/public-welfare/public-welfare-activity/list?typeId=${e.id}`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>
