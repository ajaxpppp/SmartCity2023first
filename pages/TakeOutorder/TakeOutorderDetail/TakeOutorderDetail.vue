<template>
	<view>
		<view>
			<view>
				<image :src="$u.a+item.imgUrl" style="margin-right: 20rpx;" mode="">
				</image>
			</view>
			<view>
				<view style="font-weight: bold;">{{item.name}}</view>
				<view style="font-size: 1rpx; display: flex;">评分:<uni-rate :value="item.score"></uni-rate>
				</view>
				<view>月销量:{{item.saleQuantity}}</view>
				<view>人均消费:{{item.distance}}</view>
				<view style="display: flex;">店家收藏:<uni-fav :checked="checked" @click="onClick(item.id)" /></view>
			</view>
		</view>

		<uni-section title="新闻专栏" sub-title="" type="line">

			<view v-for="(item,index) in list" :key="index">
				<uni-card>
					<navigator :url="`../MenuDetailsPage/MenuDetailsPage?id=${JSON.stringify(item)}`"
						style="height: 100%;">
						<view style="display: flex;">
							<view>
								<image :src="$u.a+item.imgUrl"
									style="width: 320rpx; height: 320rpx; margin-right: 20rpx;" mode=""></image>
							</view>
							<view>
								<view style="font-weight: bold;">名称:{{item.name}}</view>
								<view>价格:{{item.price}}元</view>
								<view style="font-size: 1rpx; display: flex;">评分:<uni-rate value="5"></uni-rate>
								</view>
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
				item: [],
				checked: null,
				list: []
			}
		},
		methods: {
			onClick(e) {
				this.$r.h(`/prod-api/api/takeout/collect/check?sellerId=${e}`).then(res => {

					if (res.isCollect == false) {
						this.$r.h(`/prod-api/api/takeout/collect`, 'post', {
							"sellerId": e
						}).then(res => {
							uni.showToast({
								title: '收藏成功'
							});
						})
					} else {
						this.$r.h(`/prod-api/api/takeout/collect/${e}`, 'DELETE').then(res => {
							uni.showToast({
								title: '取消收藏'
							});
						})
					}
				})
			}
		},
		onLoad(e) {
			this.$r.h(`/prod-api/api/takeout/seller/${e.id}`).then(res => {
				this.item = res.data
				if (res.code == 200) {
					this.$r.h(`/prod-api/api/takeout/collect/check?sellerId=${this.item.id}`).then(res => {
						this.checked = res.isCollect
						console.log("res: " + JSON.stringify(res));
					})
				}
			})

			this.$r.h(`/prod-api/api/takeout/product/list?sellerId=1&categoryId=19`).then(res => {
				this.list = res.data
			})
		}
	}
</script>

<style>

</style>