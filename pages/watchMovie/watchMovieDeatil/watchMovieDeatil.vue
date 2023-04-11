<template>
	<view>
		<uni-section title="电影信息详情" sub-title="" type="line">
			<view>
				<uni-card>
					<view style="display: flex;">
						<view>
							<image :src="$u.a+item.cover" style="width: 320rpx; height: 320rpx; margin-right: 20rpx;"
								mode=""></image>
						</view>
						<view>
							<view>电影名称:{{item.name}}</view>
							<view>评分:{{item.score}}分</view>
							<view>上映时间:{{item.playDate}}</view>
							<view>想看人数:{{item.favoriteNum}}</view>
						</view>
					</view>
				</uni-card>
				<navigator url="../watchMovie"><button type="primary">主页</button></navigator>
			</view>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				item: []
			}
		},
		methods: {

		},
		onLoad(e) {
			this.$r.h(`/prod-api/api/movie/film/detail/${e.id}`).then(res => {
				this.item = res.data
			})
		}
	}
</script>

<style>

</style>