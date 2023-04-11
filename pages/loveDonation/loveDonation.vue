<template>
	<view>
		<uni-search-bar placeholder="请输入内容" @confirm="confirm"></uni-search-bar>

		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,index) in sp" :key="index">
				<navigator :url="`newDetail/newDetail?id=${item.id}`" style="height: 100%;">
					<image :src="$u.a+item.imgUrl" style="width: 100%; height: 100%;" mode=""></image>
				</navigator>
			</swiper-item>
		</swiper>

		<uni-section title="公益分类" sub-title="" type="line">
			<uni-grid :column="4" :showBorder="false">
				<uni-grid-item v-for="(item,index) in icon" :key="index">
					<view class="imgs">
						<image :src="$u.a+item.imgUrl" style="width: 80rpx; height: 80rpx; border-radius: 50%;" mode="">
						</image>
						<view>{{item.name}}</view>
					</view>
				</uni-grid-item>
			</uni-grid>
		</uni-section>

		<uni-section title="推荐列表项" sub-title="" type="line">

			<uni-row>
				<uni-col :span="24/text.length" v-for="(item,index) in text" :key="index">
					<view @click="textc(item.id)" style="text-align: center;" :style="id==item.id?'color:blue':''">
						{{item.name.slice(0,2)}}
					</view>
				</uni-col>
			</uni-row>

			<view v-for="(item,index) in list" :key="index">
				<uni-card>
					<navigator :url="`loveDeonationList/loveDeonationList?id=${item.id}`" style="height: 100%;">
						<view style="display: flex;">
							<view>
								<image :src="$u.a+item.imgUrl"
									style="width: 320rpx; height: 320rpx; margin-right: 20rpx;" mode=""></image>
							</view>
							<view>
								<view style="font-weight: bold;">{{item.name}}</view>
								<view>发布组织:{{item.author}}</view>
								<view>捐赠人数:{{item.donateCount}}</view>
								<view>已筹善款:{{item.moneyNow}}</view>
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
				sp: [],
				icon: [],
				list: [],
				text: [],
				id: 10
			}
		},
		methods: {
			confirm(e) {
				uni.navigateTo({
					url: '/pages/index/serachList/serachList?id=' + e.value
				})
			},
			textc(e) {
				this.id = e
				this.$r.h(`/prod-api/api/public-welfare/public-welfare-activity/list?typeId=${this.id}`).then(
					res => {
						this.list = res.rows
					})
			}
		},
		onLoad() {
			this.textc(this.id)
			this.$r.h(`/prod-api/api/public-welfare/ad-banner/list`).then(res => {
				this.sp = res.data
			})

			this.$r.h(`/prod-api/api/public-welfare/public-welfare-type/list`).then(res => {
				this.icon = res.data
			})

			// this.$r.h(`/prod-api/api/public-welfare/public-welfare-activity/recommend-list`).then(res => {
			// 	this.list = res.rows
			// })

			this.$r.h('/prod-api/api/public-welfare/public-welfare-type/list').then(res => {
				this.text = res.data
			})
		}
	}
</script>

<style>

</style>
