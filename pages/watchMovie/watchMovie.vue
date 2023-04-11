<template>
	<view>
		<view>
			<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
				<swiper-item v-for="item in zh22">
					<image :src="$u.a+item.advImg" style="width: 100%;" mode="widthFix"></image>
				</swiper-item>
			</swiper>
		</view>
		<uni-search-bar placeholder="搜索" v-model="title" @confirm="confirm"></uni-search-bar>
		<uni-section title="电影展示区列表" sub-title="" type="line">
			<view v-for="(item,index) in zh2234" :key="index">
				<uni-card>
					<navigator :url="`watchMovieDeatil/watchMovieDeatil?id=${item.id}`" style="height: 100%;">
						<view style="display: flex;">
							<view>
								<image :src="$u.a+item.cover"
									style="width: 320rpx; height: 320rpx; margin-right: 20rpx;" mode=""></image>
							</view>
							<view>
								<view>影片名称:{{item.name}}</view>
								<view>上映时间:{{item.playDate}}</view>
								<view>时长:{{item.duration}}分钟</view>
								<view>评分:{{item.score}}分</view>
								<view>想看人数:{{item.favoriteNum}}</view>
							</view>
						</view>
					</navigator>
				</uni-card>
			</view>
		</uni-section>

		<button type="primary" @click="ppsi" v-if="indexs==5">查看更多</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				zh22: [],
				title: "",
				zh2234: [],
				indexs: 5
			}
		},
		methods: {
			confirm(e) {
				this.$r.h(`/prod-api/api/movie/film/list?name=${e.value}`).then(res => {
					this.zh2234 = res.rows
				})
			},
			ppsi() {
				this.indexs += 100
				this.$r.h(`/prod-api/api/movie/film/list?pageNum=0&pageSize=${this.indexs}`).then(res => {
					this.zh2234 = res.rows
				})
			}
		},
		onLoad() {
			this.$r.h(`/prod-api/api/movie/rotation/list`).then(res => {
				this.zh22 = res.rows
			})
			this.$r.h(`/prod-api/api/movie/film/list?pageNum=0&pageSize=${this.indexs}`).then(res => {
				this.zh2234 = res.rows
			})
		},
		onBackPress: () => {
			uni.switchTab({
				url: '/pages/index/index'
			})
		},
	}
</script>

<style>

</style>