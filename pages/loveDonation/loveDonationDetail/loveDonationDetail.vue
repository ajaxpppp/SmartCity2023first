<template>
	<view>
		<image :src="$u.a+item.imgUrl" mode=""></image>
		<view style="text-align: center;">
			<view>项目名称:{{item.name}}</view>
			<view>已募善款:{{item.moneyNow}}</view>
			<view>筹款目标:{{item.moneyTotal}}</view>
			<view>项目备案号:湘10086</view>
			<view>参与人数:{{item.donateCount}}人</view>
			<view>捐款进度:700%</view>
			<view>项目时间:{{item.createTime}}</view>
		</view>

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
			this.item = JSON.parse(e.id)
		}
	}
</script>

<style>

</style>
