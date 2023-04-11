<template>
	<view>

		<uni-section title="地址管理" sub-title="" type="line">
			<uni-forms ref="form" style="padding: 100rpx;">
				<uni-forms-item label="姓名" name="">
					<uni-easyinput v-model="name" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="电话">
					<uni-easyinput v-model="phone" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="标签" name="">
					<uni-easyinput v-model="label" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="详细地址">
					<uni-easyinput v-model="addressDetail" placeholder="" />
				</uni-forms-item>
			</uni-forms>
			<button type="primary" @click="addAddress">添加收获地址</button>
		</uni-section>
		<uni-section title="我的收藏" sub-title="" type="line">
			<view v-for="(item,index) in list.slice(0,3)" :key="index">
				<uni-card>
					<navigator :url="`TakeOutorderDetail/TakeOutorderDetail?id=${item.id}`" style="height: 100%;">
						<view style="display: flex;">
							<view>
								<image :src="$u.a+item.imgUrl"
									style="width: 320rpx; height: 320rpx; margin-right: 20rpx;" mode=""></image>
							</view>
							<view>
								<view style="font-weight: bold;">{{item.sellerName}}</view>
								<view>店家简介:{{item.address}}</view>
								<view>店家评分:<uni-rate :value="item.score"></uni-rate></view>
							</view>
						</view>
					</navigator>
				</uni-card>
			</view>
		</uni-section>



		<view
			style="position: fixed; bottom: 0; background-color: #ffffff; height: 120rpx; width: 100%; margin: 0 auto;">
			<uni-grid :column="3" :showBorder="false">
				<uni-grid-item>
					<navigator url="../TakeOutorder">
						<view class="imgs">
							<image src="../../../static/volun/bus2.png" style="width: 80rpx ; height: 80rpx;" mode="">
							</image>
							<view>首页</view>
						</view>
					</navigator>
				</uni-grid-item>

				<uni-grid-item>
					<navigator url="../Deliveryorder/Deliveryorder">
						<view class="imgs">
							<image src="../../../static/volun/bus2.png" style="width: 80rpx ; height: 80rpx;" mode="">
							</image>
							<view>订单</view>
						</view>
					</navigator>
				</uni-grid-item>

				<uni-grid-item>
					<navigator>
						<view class="imgs">
							<image src="../../../static/volun/bus2.png" style="width: 80rpx ; height: 80rpx;" mode="">
							</image>
							<view style="color: red;">我的</view>
						</view>
					</navigator>
				</uni-grid-item>
			</uni-grid>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [],
				"addressDetail": "大连理工大学教学楼 A3-118",
				"label": "学校",
				"name": "王大卫",
				"phone": "15898135276"
			}
		},
		methods: {
			addAddress() {

				this.$r.h(`/prod-api/api/takeout/address`, 'post', {
					"addressDetail": this.addressDetail,
					"label": this.label,
					"name": this.name,
					"phone": this.phone
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: '收藏成功'
						});
					} else {
						uni.showToast({
							title: res.msg
						});
					}
				})
			}
		},
		onLoad() {
			this.$r.h(`/prod-api/api/takeout/collect/list`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>