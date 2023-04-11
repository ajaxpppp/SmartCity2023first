<template>
	<view>
		<button type="primary" @click="add">随手拍</button>

		<view>
			<image :src="item" v-for="(item,index) in list" :key="index" mode=""></image>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: ['../../../static/partyBuilding/(1).jpg',
					'../../../static/partyBuilding/(2).jpg',
					'../../../static/partyBuilding/(3).jpg',
					'../../../static/partyBuilding/(4).jpg',
				]
			}
		},
		methods: {
			add() {
				uni.chooseImage({
					count: 1,
					success: (res) => {
						console.log("res.: " + JSON.stringify(res.tempFilePaths));
					}
				})
			}
		}
	}
</script>

<style>

</style>