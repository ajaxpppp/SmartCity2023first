<template>
	<view>
		<uni-section title="述求列表" sub-title="" type="line">
			<view v-for="(item,index) in list.slice(0,10)" :key="index"
				style="display: flex; margin: 20rpx; font-size: 18rpx;">
				<navigator :url="`../hotLineDetail/hotLineDetail?id=${item.id}&temp=${temp}`">
					<view style="margin-left: 20rpx;">
						<view style="font-weight: bold;">标题:{{item.title}}</view>
						<view>承办单位:{{item.undertaker}}</view>
						<view>提交时间:{{item.createTime}}</view>
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
				list: [],
				temp: 0,
			}
		},
		methods: {

		},
		onLoad(e) {
			this.temp = e.id
			this.$r.h(`/prod-api/api/gov-service-hotline/appeal/list?appealCategoryId=` + e.id).then(res => {
				this.list = res.rows.sort(function(a, b) {
					return new Date(b.createTime).getTime() - new Date(a.createTime).getTime()
				})
			})
		}
	}
</script>

<style>

</style>
