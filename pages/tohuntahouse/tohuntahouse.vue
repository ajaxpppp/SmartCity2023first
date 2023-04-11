<template>
	<view>
		<uni-search-bar @confirm="confirm" @input="" placeholder="请输入房源名称" />
		<view>

			<uni-section title="房源展示分类" sub-title="" type="line">
				<uni-grid :column="4" :showBorder="false">
					<uni-grid-item v-for="(item,index) in icon" :key="index">
						<view @click="top(item.name)"
							style="display: flex; justify-content: center; align-items: center; flex-direction: column; height: 100%;">
							<image :src="item.url" style="width: 80rpx; height: 80rpx;" mode=""></image>
							<view>{{item.name}}</view>
						</view>
					</uni-grid-item>
				</uni-grid>
			</uni-section>



			<view v-for="(item,index) in list" :key="index">
				<navigator style="height: 100%;" :url="`tohunthouseDeatil/tohunthouseDeatil?id=${item.id}`">
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
										<view class="text">
											房源简介:{{item.description?item.description.slice(0,25)+"...":''}}
										</view>
									</view>
								</view>
							</template>
						</uni-list-item>
					</uni-list>
				</navigator>
			</view>
			</uni-section>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				icon: [{
						url: '../../static/house/1.png',
						name: "二手"
					},
					{
						url: '../../static/house/2.png',
						name: "租房"
					},
					{
						url: '../../static/house/3.png',
						name: "楼盘"
					},
					{
						url: '../../static/house/4.png',
						name: "中介"
					},
				],
				list: []
			}

		},
		methods: {
			confirm(e) {
				uni.navigateTo({
					url: "tohunthouseserach/tohunthouseserach?id=" + e.value
				})
			},

			top(e) {
				this.$r.h(`/prod-api/api/house/housing/list?houseType=` + e).then(res => {
					this.list = res.rows
				})
			}
		},
		onLoad() {
			this.top('二手')
		},
		onBackPress() {
			uni.reLaunch({
				url: '../index/index'
			})
		}
	}
</script>

<style>

</style>
