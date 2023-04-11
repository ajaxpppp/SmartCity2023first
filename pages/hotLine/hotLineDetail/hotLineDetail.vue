<template>
	<view>
		<view style="text-align: center;">
			<view>标题:{{item.title}}</view>
			<view>内容:{{item.content}}</view>
			<image :src="$u.a+`/prod-api/`+item.imgUrl" style="width: 100%;" mode=""></image>
			<view>承办单位:{{item.undertaker}}</view>
			<view>提交时间:{{item.createTime}}</view>
			<view v-if="item.state==1">处理状态:已处理</view>
			<view else>处理状态:未处理</view>
			<view>处理结果:{{item.detailResult}}</view>
			<navigator :url="`../addhotLine/addhotLine?id=${item.id}&temp=${temp}`" style="height: 100%;"> <button
					type="primary" style="margin: 50rpx;">述求发布</button>
			</navigator>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				item: [],
				temp: 0
			}
		},
		methods: {

		},
		onLoad(e) {
			this.temp = e.temp
			this.$r.h(`/prod-api/api/gov-service-hotline/appeal/` + e.id).then(res => {
				this.item = res.data
			})
		}
	}
</script>

<style>

</style>
