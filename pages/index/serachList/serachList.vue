<template>
	<view>
		<view v-for="(item,index) in list" :key="index">
			<uni-card>
				<navigator :url="`../newDetail/newDetail?id=${item.id}`" style="height: 100%;">
					<view style="display: flex;">
						<view>
							<image :src="$u.a+item.cover" style="width: 320rpx; height: 320rpx; margin-right: 20rpx;"
								mode=""></image>
						</view>
						<view>

							<view style="font-weight: bold;">{{item.title}}</view>
							<rich-text :nodes="item.content?item.content.slice(0,30)+'...':''"></rich-text>
							<view>评论总数:{{item.commentNum}}</view>
							<view>发布时间:{{item.publishDate}}</view>
						</view>
					</view>
				</navigator>
			</uni-card>
		</view>
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
			this.$r.h(`/prod-api/press/press/list?title=${e.id}`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>
