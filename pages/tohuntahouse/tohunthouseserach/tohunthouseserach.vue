<template>
	<view>

		<view v-for="(item,index) in list" :key="index" @click="tode(item.id)">
			<navigator style="height: 100%;" :url="`../tohunthouseDeatil/tohunthouseDeatil?id=${item.id}`">
				<uni-list>
					<uni-list-item title="" note="">
						<template v-slot:body>
							<view>
								<image
									style="width: 300rpx; height: 200rpx; margin:0 20rpx 0 20rpx; border-radius: 10rpx;"
									:src="$u.a+item.pic" mode=""></image>
							</view>
							<view style="font-size: 18rpx;">
								<view>
									<view style="font-weight: bold;">所在小区名称{{item.sourceName}}</view>

									<view>房源面积:{{item.areaSize}}</view>
									<view>价格:{{item.price}}</view>
									<view class="text">房源简介:{{item.description?item.description.slice(0,25)+"...":''}}
									</view>
								</view>
							</view>
						</template>
					</uni-list-item>
				</uni-list>
			</navigator>
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
			tode(e) {
				uni.navigateTo({
					url: '../deila/deila?id=' + e
				})
			}
		},
		onLoad(e) {
			this.$r.h(`/prod-api/api/house/housing/list?sourceName=` + e.id).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>
