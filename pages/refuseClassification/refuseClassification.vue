<template>
	<view>
		<view>
			<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
				<swiper-item v-for="(item,index) in sp" :key="index">
					<image :src="$u.a+item.imgUrl" style="height: 100%;" mode=""></image>
				</swiper-item>
			</swiper>
		</view>

		<uni-section title="导航" sub-title="" type="line">
			<uni-grid :column="2" :showBorder="false">
				<navigator url="refusesearch/refusesearch">
					<uni-grid-item>
						<view class="imgs">
							<image style="width: 320rpx; height: 220rpx; border-radius: 20rpx;"
								src="../../static/refuseimg/5.jpg" mode="">
							</image>
							<view class="text">搜索</view>
						</view>
					</uni-grid-item>
				</navigator>

				<navigator url="refuseclassify/refuseclassify">
					<uni-grid-item>
						<view class="imgs">
							<image style="width: 320rpx; height: 220rpx; border-radius: 20rpx;"
								src="../../static/refuseimg/1.jpeg" mode=""></image>
							<view class="text">分类</view>
						</view>
					</uni-grid-item>
				</navigator>
			</uni-grid>
		</uni-section>


		<uni-section title="新闻资讯" sub-title="" type="line">
			<view>
				<uni-row>
					<uni-col :span="24/icon.length" v-for="(item,index) in icon">
						<view style="text-align: center;" @click="toot(item.id)" :style="item.id==id?'color:blue':''">
							{{item.name}}
						</view>
					</uni-col>
				</uni-row>
			</view>

			<view v-for="(item,index) in list" :key="index">
				<navigator :url="`refuseClassificationDeatil/refuseClassificationDeatil?id=${item.id}`">
					<uni-card>
						<view style="display: flex;">
							<view>
								<view style="font-weight: bold;">{{item.title}}</view>
								<view>发布时间:{{item.createTime}}</view>
								<view>{{item.content}}</view>
							</view>
							<view>
								<image :src="$u.a+item.imgUrl"
									style="width: 320rpx; height:220rpx; margin-right: 20rpx; margin-left: 20rpx;"
									mode=""></image>
							</view>
						</view>
					</uni-card>
				</navigator>
			</view>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				sp: [],
				icon: [],
				hot: [],
				text: [],
				list: [],
				id: 7
			}
		},
		methods: {
			toot(e) {
				this.id = e
				this.$r.h(`/prod-api/api/garbage-classification/news/list?type=` + e).then(res => {
					this.list = res.rows
				})
			},
		},
		onLoad() {
			this.toot(this.id)
			this.$r.h(`/prod-api/api/garbage-classification/ad-banner/list`).then(res => {
				this.sp = res.data
			})

			this.$r.h(`/prod-api/api/garbage-classification/news-type/list`).then(res => {
				this.icon = res.rows
			})

			this.$r.h(`/prod-api/press/press/list?hot=Y`).then(res => {
				this.hot = res.rows
			})

			this.$r.h(`/prod-api/press/category/list`).then(res => {
				this.text = res.data
			})
		}
	}
</script>

<style>

</style>
