<template>
	<view>
		<image :src="$u.a+item.coverImgUrl" v-if="item.id==8" v-for="(item,index) in list" :key="index" mode="">
		</image>
		<uni-section title="标志性建筑" sub-title="" type="line">
			<uni-grid :column="3" :showBorder="false">
				<uni-grid-item v-for="(item,index) in icon" :key="index">
					<navigator :url="`policy/policy?id=${item.id}`">
						<view class="imgs">
							<image style=" width: 210rpx; height: 210rpx;" :src="$u.a+item.imgUrl" mode=""></image>
							<view style="text-align: center;">{{item.name}}</view>
						</view>
					</navigator>
				</uni-grid-item>
			</uni-grid>
		</uni-section>
		<uni-section title="青年驿站列表" sub-title="" type="line">
			<view v-for="(item,index) in list" :key="index">
				<uni-card>
					<navigator :url="`youthDetail/youthDetail?id=${item.id}`">
						<view style="display: flex;">
							<view>
								<image :src="$u.a+item.coverImgUrl"
									style="width: 320rpx; height: 320rpx; margin-right: 20rpx;" mode=""></image>
							</view>
							<view>
								<view style="font-weight: bold;">{{item.name}}</view>
								<view>剩余男床位数:{{item.bedsCountBoy}}</view>
								<view>剩余女床位数:{{item.bedsCountGirl}}</view>
								<view>详细地址:{{item.address}}</view>
							</view>
						</view>
					</navigator>
					<view>
						<view v-if="temp==false" @click="showdetail(item.id)">驿站详情:{{item.introduce}}</view>
						<button type="primary" @click="showdetail(item.id)" v-if="temp==true">站点介绍</button>
					</view>
				</uni-card>
			</view>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [],
				icon: [],
				temp: true,
				id: 0
			}
		},
		methods: {
			showdetail(e) {
				if (this.temp == true) {
					this.temp = false
				} else {
					this.temp = true
				}
			}
		},
		onLoad() {
			this.$r.h(`/prod-api/api/youth-inn/youth-inn/list`).then(res => {
				this.list = res.rows
			})

			this.$r.h(`/prod-api/api/youth-inn/talent-policy-area/list`).then(res => {
				this.icon = res.data
			})
		}
	}
</script>

<style>

</style>
