<template>
	<view>
		<view v-for="(item,index) in list" :key="index">
			<image :src="$u.a+item.imgUrl" mode=""></image>
			<uni-section title="分类文字描述" sub-title="" type="line">
				<view>{{item.guide}}</view>
			</uni-section>
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

		},
		onLoad(e) {

			this.$r.h(`/prod-api/api/garbage-classification/garbage-classification/list?Name=${e.id}`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>
