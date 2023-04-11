<template>
	<view>
		<uni-section title="停车场详情" sub-title="" type="line">
			<uni-list>
				<uni-list-item
					:title="`停车场名:${item.parkName}\n空位数量:${item.vacancy}个\n地址:${item.address}\n收费价格:${item.rates}元/小时\n距离:${item.distance}米\n是否开放:${item.open=='Y'?'开放':'未开放'}`"
					note="">
				</uni-list-item>
			</uni-list>
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
			this.$r.h(`/prod-api/api/park/lot/` + e.id).then(res => {
				this.item = res.data
			})
		}
	}
</script>

<style>

</style>
