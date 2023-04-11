<template>
	<view>
		<uni-section title="当前线路名称" sub-title="" type="line">
			<view>
				<uni-group :title="dt.name" margin-top="">
					<view>线路名称:{{dt.name}}</view>
					<view>始发站:{{dt.first}}</view>
					<view>终点站:{{dt.end}}</view>
					<view>剩余时间:{{dt.startTime}}-{{dt.endTime}}</view>
					<view>剩余:2站</view>
					<view>剩余距离:{{dt.km}}千米</view>
				</uni-group>
			</view>
			<scroll-view scroll-x="true">
				<uni-breadcrumb separator="-->">
					<uni-breadcrumb-item style="margin: 50rpx; font-size: 50rpx;"
						v-for="(item,index) in dt.metroStepList" :key="index">
						<view :style="item.name=='积水潭'?'color:red':''">{{item.name}}</view>
					</uni-breadcrumb-item>
				</uni-breadcrumb>
			</scroll-view>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				dt: [],
				list: []
			}
		},
		methods: {

		},
		onLoad(e) {
			this.$r.h(`/prod-api/api/metro/line/` + e.id).then(res => {
				this.dt = res.data
			})

			// this.$r.h(`/prod-api/api/metro/list?currentName=建国门`).then(res => {
			// 	let lili = res.data
			// 	console.log("lili: " + JSON.stringify(lili));
			// 	for (let s of lili) {
			// 		this.$r.h(`/prod-api/api/metro/line/${s.lineId}`).then(res => {
			// 			this.list = res.data
			// 			console.log("res: " + JSON.stringify(res));
			// 		})
			// 	}
			// })

		}
	}
</script>

<style>

</style>