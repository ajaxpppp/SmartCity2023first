<template>
	<view>
		<uni-grid :column="4" :showBorder="false">
			<uni-grid-item v-for="(item,index) in icon" :key="index">
				<navigator :url="`../LegalexpertiseList/LegalexpertiseList?id=${item.id}`" style="height: 100%;">
					<view
						style="height: 100%; display: flex; justify-content: center; align-items: center; flex-direction: column;">
						<image :src="$u.a+item.imgUrl" style="width: 80rpx; height: 80rpx;" mode="">
						</image>
						<view>{{item.name}}</view>
					</view>
				</navigator>
			</uni-grid-item>
		</uni-grid>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				icon: []
			}
		},
		methods: {

		},
		onLoad() {
			this.$r.h(`/prod-api/api/lawyer-consultation/legal-expertise/list`).then(res => {
				this.icon = res.rows.sort(function(a, b) {
					return b.sort - a.sort
				})
			})
		}
	}
</script>

<style>

</style>
