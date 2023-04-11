<template>
	<view>
		<uni-section title="店家列表" sub-title="" type="line">
			<view v-for="(item,index) in list" :key="index">
				<uni-card>
					<navigator :url="`../TakeOutorderDetail/TakeOutorderDetail?id=${item.id}`" style="height: 100%;">
						<view style="display: flex;">
							<view>
								<image :src="$u.a+item.imgUrl"
									style="width: 320rpx; height: 320rpx; margin-right: 20rpx;" mode=""></image>
							</view>
							<view>
								<view style="font-weight: bold;">{{item.name}}</view>
								<view style="font-size: 1rpx; display: flex;">评分:<uni-rate
										:value="item.score"></uni-rate></view>
								<view>月销量:{{item.saleQuantity}}</view>
								<view>到店所需时间:{{item.deliveryTime}}</view>
								<view>人均消费:{{item.distance}}</view>
							</view>
						</view>
					</navigator>
				</uni-card>
			</view>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: []
			}
		},
		methods: {

		},
		onLoad(e) {
			this.$r.h(`/prod-api/api/takeout/seller/list?&themeId=${e.id}`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>