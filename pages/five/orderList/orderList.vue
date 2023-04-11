<template>
	<view>
		<uni-segmented-control :current="current" :values="list" @clickItem="clickItem"></uni-segmented-control>
		<view class="content">
			<view v-show="current === 0">
				<uni-list v-for="(item,index) in listc" :key="index">
					<uni-list-item
						:title="`路线名称:${item.path}\n起终点:${item.start}~${item.end}\n票价:${item.price}元\n订单编号:${item.orderNum}\n乘车日期:${item.payTime}`"
						note=""></uni-list-item>
					<navigator :url="`orderpay/orderpay?id=${JSON.stringify(item)}`"> <button
							type="primary">支付订单</button></navigator>
				</uni-list>
			</view>
			<view v-show="current === 1">
				<uni-list v-for="(item,index) in listc" :key="index" v-if="item.status==1">
					<uni-list-item
						:title="`路线名称:${item.path}\n起终点:${item.start}~${item.end}\n票价:${item.price}元\n订单编号:${item.orderNum}\n乘车日期:${item.payTime}`"
						note=""></uni-list-item>
				</uni-list>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				current: 0,
				list: ["未处理", '已处理'],
				listc: []
			}
		},
		methods: {
			clickItem(e) {
				this.current = e.currentIndex
			}
		},
		onShow() {
			this.$r.h(`/prod-api/api/bus/order/list`).then(res => {
				this.listc = res.rows.sort(function(a, b) {
					return b.payTime > a.payTime ? 1 : -1
				})
			})
		}
	}
</script>

<style>

</style>