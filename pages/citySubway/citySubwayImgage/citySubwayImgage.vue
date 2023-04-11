<template>
	<view>
		<image :src="$u.a+img.imgUrl" style="width: 100%; height: 100vh; " mode=""></image>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				img: []
			}
		},
		methods: {

		},
		onLoad() {
			this.$r.h(`/prod-api/api/metro/city`).then(res => {
				this.img = res.data
			})
		}
	}
</script>

<style>

</style>