<template>
	<view>
		<uni-segmented-control :current="current" :values="offices" @clickItem="clickItem"></uni-segmented-control>
		<view class="content">
			<view v-show="current === 0">
				暂无数据
			</view>
			<view v-show="current === 1">
				<uni-card v-for="(item,index) in list" :key="index">
					<view>预约科室:{{item.categoryName}}</view>
					<view>门诊类型:普通</view>
					<view>预约时间:{{$r.getDate()}}</view>
					<navigator
						:url="`../RegistrationInformation/RegistrationInformation?id=${item.id}&name=${item.categoryName}`">
						<button type="primary" plain="">预约</button>
					</navigator>
				</uni-card>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				current: 0,
				offices: ['专家', '普通'],
				list: [],
				data: ""
			}
		},
		methods: {
			clickItem(e) {
				this.current = e.currentIndex
			}
		},
		onLoad() {
			this.data = new Date().toLocaleDateString()
			console.log("this.data: " + JSON.stringify(this.data));
			this.$r.h(`/prod-api/api/hospital/category/list`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>
