<template>
	<view>
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,index) in sp" :key="index">
				<image :src="$u.a+item.imgUrl" style="height: 100%;" mode=""></image>
			</swiper-item>
		</swiper>
		<uni-search-bar @confirm="confirm" @input="" placeholder="输入分类" />
		<uni-section title="热门搜索" sub-title="" type="line">
			<uni-list v-for="(item,index) in hot.slice(0,5)" :key="index">
				<uni-list-item :title="`关键词:${item.keyword}`" note=""></uni-list-item>
			</uni-list>
		</uni-section>


		<uni-section title="常见垃圾物品" sub-title="" type="line">
			<uni-grid :column="4" :showBorder="false">
				<uni-grid-item v-for="(item,index) in icon.slice(0,16)" :key="index">
					<navigator :url="`../incommonuse/incommonuse?id=${item.type}`">
						<view class="imgs">
							<image style="width: 80rpx; height: 80rpx; border-radius: 50rpx;" :src="$u.a+item.imgUrl"
								mode="">
							</image>
							<view>{{item.name}}</view>
						</view>
					</navigator>
				</uni-grid-item>
			</uni-grid>
		</uni-section>


		<uni-section title="可回收投放指导" sub-title="" type="line">
			<view v-for="(item,index) in list" :key="index" v-if="item.name!='有害垃圾'">
				<uni-list>
					<uni-list-item title="" note="">
						<template v-slot:body>
							<view style="display: flex;">
								<view>
									<image
										style="width: 320rpx; height: 220rpx; border-radius: 10rpx; margin-right: 20rpx;"
										:src="$u.a+item.imgUrl" mode=""></image>
								</view>
								<view>
									<view>投放指导:{{item.guide}}</view>
								</view>
							</view>
						</template>
					</uni-list-item>
				</uni-list>
			</view>
		</uni-section>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				sp: [],
				icon: '',
				list: [],
				hot: []
			}
		},
		methods: {
			confirm(e) {
				uni.navigateTo({
					url: "/pages/refuseClassification/searchclassify/searchclassify?id=" + e.value
				})
			}
		},
		onLoad(e) {
			this.$r.h(`/prod-api/api/garbage-classification/poster/list`).then(res => {
				this.sp = res.data
			})
			this.$r.h(`/prod-api/api/garbage-classification/garbage-example/list`).then(res => {
				this.icon = res.rows
			})

			this.$r.h(`/prod-api/api/garbage-classification/garbage-classification/list`).then(res => {
				this.list = res.rows
			})

			this.$r.h(`/prod-api/api/garbage-classification/garbage-classification/hot/list`).then(res => {
				this.hot = res.data.sort(function(a, b) {
					return b.searchTimes > a.searchTimes ? 1 : -1
				})
			})
		}
	}
</script>

<style>

</style>
