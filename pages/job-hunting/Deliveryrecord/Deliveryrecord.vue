<template>
	<view>

	</view>
</template>

<script>
	export default {
		data() {
			return {

			}
		},
		methods: {

		},
		onLoad() {
			this.$r.h(`/prod-api/api/job/deliver/list`).then(res => {
				console.log("res: " + JSON.stringify(res));
			})
		}
	}
</script>

<style>

</style>