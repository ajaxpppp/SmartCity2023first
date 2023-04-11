<template>
	<view>
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,index) in sp" :key="index">
				<image :src="$u.a+item.imgUrl" style="height: 100%;" mode=""></image>
			</swiper-item>
		</swiper>

		<uni-section title="医院简介" sub-title="" type="line">
			<rich-text :nodes="item.brief"></rich-text>
		</uni-section>

		<navigator :url="`../haveanappointmentwithadoctor/haveanappointmentwithadoctor?id=${id}`"><button
				type="primary">预约挂号</button></navigator>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				sp: [],
				item: [],
				id: 0,
			}
		},
		methods: {

		},
		onLoad(e) {
			this.id = e.id
			this.$r.h(`/prod-api/api/hospital/banner/list?hospitalId=${e.id}`).then(res => {
				this.sp = res.data
			})

			this.item = JSON.parse(e.item)
		}
	}
</script>

<style>

</style>
