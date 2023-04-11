<template>
	<view>
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,index) in sp" :key="index">
				<image @click="tonewdetials(item.id)" :src="$u.a+item.advImg" style="width: 100%; height: 100%;">
				</image>
			</swiper-item>
		</swiper>
		<uni-section title="当前位置" sub-title="" type="line">
			北京建国门站位置
		</uni-section>


		<view v-for="(item,index) in dt" :key="index">
			<navigator :url="`citySubwayDeatil/citySubwayDeatil?id=${item.lineId}`">
				<uni-group :title="item.currentName" margin-top="20">
					<view>线路:{{item.lineName}}</view>
					<view>下一站:{{item.nextStep.name}}</view>
					<view>上一站:{{item.preStep.name}}</view>
					<view>到站时长:{{item.reachTime}}小时</view>
				</uni-group>
			</navigator>
		</view>


	</view>
</template>

<script>
	export default {
		data() {
			return {
				sp: [],
				dt: []
			}
		},
		methods: {
			toss(e) {

			}
		},
		onLoad() {
			this.$r.h(`/prod-api/api/metro/rotation/list`).then(res => {
				this.sp = res.rows
			})
			this.$r.h(`/prod-api/api/metro/list?currentName=建国门`).then(res => {
				this.dt = res.data
			})
		}
	}
</script>

<style>

</style>