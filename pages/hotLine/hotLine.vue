<template>
	<view>
		<view>
			<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
				<swiper-item v-for="(item,index) in sp" :key="index">
					<image :src="$u.a+item.imgUrl" style="width: 100%; height: 100%;" mode=""></image>
				</swiper-item>
			</swiper>
		</view>

		<uni-section title="市民诉求分类" sub-title="" type="line">
			<view>
				<swiper style="height: 30vh;" :indicator-dots="true">
					<swiper-item>
						<uni-grid :column="4" :showBorder="false">
							<uni-grid-item v-for="(item,index) in icon.slice(0,8)" :key="index">
								<navigator :url="`hotLinelist/hotLinelist?id=${item.id}`" style="height: 100%;">
									<view
										style="height: 100%; display: flex; justify-content: center; align-items: center; flex-direction: column;">
										<image :src="$u.a+item.imgUrl" style="width: 80rpx; height: 80rpx;" mode="">
										</image>
										<view>{{item.name}}</view>
									</view>
								</navigator>
							</uni-grid-item>
						</uni-grid>
					</swiper-item>
					<swiper-item>
						<uni-grid :column="4" :showBorder="false">
							<uni-grid-item v-for="(item,index) in icon.slice(8,16)" :key="index">
								<navigator :url="`hotLinelist/hotLinelist?id=${item.id}`" style="height: 100%;">
									<view
										style="height: 100%; display: flex; justify-content: center; align-items: center; flex-direction: column;">
										<image :src="$u.a+item.imgUrl" style="width: 80rpx; height: 80rpx;" mode="">
										</image>
										<view>{{item.name}}</view>
									</view>
								</navigator>
							</uni-grid-item>
						</uni-grid>
					</swiper-item>
				</swiper>
			</view>
		</uni-section>




		<uni-section title="我的述求" sub-title="" type="line">
			<view v-for="(item,index) in list.slice(0,10)" :key="index"
				style="display: flex; margin: 20rpx; font-size: 18rpx;">
				<navigator style="height: 100%;" :url="`hotLineDetail/hotLineDetail?id=${item.id}`">
					<view style="margin-left: 20rpx;">
						<view style="font-weight: bold;">标题:{{item.title}}</view>
						<!-- <rich-text :nodes="item.content" class="title"></rich-text> -->
						<view>承办单位:{{item.undertaker}}</view>
						<view>提交时间:{{item.createTime}}</view>
						<view v-if="item.state==1">处理状态:已处理</view>
						<view else>处理状态:未处理</view>
					</view>
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
				id: 9
			}
		},
		methods: {

		},
		onLoad() {
			this.$r.h(`/prod-api/api/gov-service-hotline/ad-banner/list`).then(res => {
				this.sp = res.data
			})
			this.$r.h(`/prod-api/api/gov-service-hotline/appeal/my-list`).then(res => {
				this.list = res.rows.sort(function(a, b) {
					return new Date(b.createTime).getTime() - new Date(a.createTime).getTime()
				})
			})
			this.$r.h(`/prod-api/api/gov-service-hotline/appeal-category/list`).then(res => {
				this.icon = res.rows
			})



		}
	}
</script>

<style>
	.container {
		padding: 20px;
		font-size: 14px;
		line-height: 24px;
	}
</style>
