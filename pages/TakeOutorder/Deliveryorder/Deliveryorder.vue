<template>
	<view>

		<view>暂无订单</view>
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
					<navigator>
						<view class="imgs">
							<image src="../../../static/volun/bus2.png" style="width: 80rpx ; height: 80rpx;" mode="">
							</image>
							<view style="color: red;">订单</view>
						</view>
					</navigator>
				</uni-grid-item>

				<uni-grid-item>
					<navigator url="../Mytakeout/Mytakeout">
						<view class="imgs">
							<image src="../../../static/volun/bus2.png" style="width: 80rpx ; height: 80rpx;" mode="">
							</image>
							<view>我的</view>
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

			}
		},
		methods: {

		},
		onLoad() {
			this.$r.h(`/prod-api/api/takeout/order/list`).then(res => {

			})
		}
	}
</script>

<style>

</style>