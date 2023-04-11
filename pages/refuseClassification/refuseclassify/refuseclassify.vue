<template>
	<view>
		<view v-for="(item,index) in img" :key="index">
			<image :src="$u.a+item.imgUrl" v-if="item.id==6" mode=""></image>
		</view>
		<view style="display: flex; width: 100%;">
			<uni-grid :column="4" border-color="#1a94ff" :showBorder="false">
				<uni-grid-item style="height: 150rpx;">
					<navigator :url="`../refuseClassifyType/refuseClassifyType?id=${'可回收垃圾'}`"
						style="background-color: #18BC37; height: 100%; border-radius: 20%; border: 1px solid #1a94ff;">
						<view style="position: relative; top:35%; text-align: center; ">
							可回收物
						</view>
					</navigator>
				</uni-grid-item>
				<uni-grid-item style="height: 150rpx;">
					<navigator :url="`../refuseClassifyType/refuseClassifyType?id=${'有害垃圾'}`"
						style="background-color:#ff0000; height: 100%; border-radius: 20%; border: 1px solid #1a94ff;">
						<view style="position: relative; top:35%; text-align: center; ">
							有害垃圾
						</view>
					</navigator>
				</uni-grid-item>
				<uni-grid-item style="height: 150rpx;">
					<navigator :url="`../refuseClassifyType/refuseClassifyType?id=${'厨余垃圾'}`"
						style="background-color:#ffaa00; height: 100%; border-radius: 20%; border: 1px solid #1a94ff;">
						<view style="position: relative; top:35%; text-align: center; ">
							湿垃圾
						</view>
					</navigator>
				</uni-grid-item>
				<uni-grid-item style="height: 150rpx;">
					<navigator :url="`../refuseClassifyType/refuseClassifyType?id=${'其他垃圾'}`"
						style="background-color: #00007f; height: 100%; border-radius: 20%; border: 1px solid #1a94ff;">
						<view style="position: relative; top:35%; text-align: center; ">
							干垃圾
						</view>
					</navigator>
				</uni-grid-item>
			</uni-grid>
		</view>


		<uni-section title="常见垃圾物品" sub-title="" type="line">
			<uni-grid :column="4" :showBorder="false">
				<uni-grid-item v-for="(item,index) in icon.slice(0,20)" :key="index">
					<navigator :url="`../incommonuse/incommonuse?id=${item.type}`">
						<view class="imgs" @click="imgs(item.id)">
							<image style="width: 80rpx; height: 80rpx; border-radius: 50rpx;" :src="$u.a+item.imgUrl"
								mode=""></image>
							<view>{{item.name}}</view>
						</view>
					</navigator>
				</uni-grid-item>
			</uni-grid>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				img: [],
				icon: []
			}
		},
		methods: {
			imgs(e) {
				console.log("e: " + JSON.stringify(e));
			}
		},
		onLoad() {
			this.$r.h(`/prod-api/api/garbage-classification/poster/list`).then(res => {
				this.img = res.data
			})

			this.$r.h(`/prod-api/api/garbage-classification/garbage-example/list`).then(res => {
				this.icon = res.rows
			})
		}
	}
</script>

<style>

</style>
