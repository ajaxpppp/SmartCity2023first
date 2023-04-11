<template>
	<view>
		<uni-search-bar @confirm="" @input="" />
		<image :src="$u.a+item.company.imgUrl" mode=""></image>
		<view class="ti">{{item.company.name}}</view>

		<view>投诉电话:{{item.company.phone}}</view>


		<uni-steps :options="shen" direction="column" :active="0"></uni-steps>

		<navigator url="../Logisticscomplaints/Logisticscomplaints"> <button type="primary">投诉</button> </navigator>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				item: [],
				shen: []
			}
		},
		methods: {

		},
		onLoad() {
			this.$r.h(`/prod-api/api/logistics-inquiry/logistics_info/ST0000001`).then(res => {
				this.item = res.data
				for (let s of this.item.stepList) {
					this.shen.push({
						title: s.addressAt,
						desc: s.eventAt
					})
				}

			})
		}
	}
</script>

<style>

</style>