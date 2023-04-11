<template>
	<view>
		<uni-section title="请输入入场时间" sub-title="" type="line">
			<uni-datetime-picker type="datetime" v-model="entryTime" />
		</uni-section>
		<uni-section title="请输入出场时间" sub-title="" type="line">
			<uni-datetime-picker type="datetime" v-model="outTime" />
		</uni-section>
		<button type="primary" @click="selectlot">查询</button>
		<uni-section title="所有停车场" sub-title="" type="line">
			<uni-list v-for="(item,index) in list" :key="index">
				<uni-list-item
					:title="`车牌号:${item.plateNumber}\n收费金额:${item.monetary}元/小时\n入场时间:${item.entryTime}\n出场时间:${item.outTime}\n停车场名称:${item.parkName}`"
					note="">
				</uni-list-item>
			</uni-list>
			<button type="primary" @click="addpark" v-if="temp!=24">查看更多</button>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [],
				entryTime: "",
				outTime: "",
				temp: 6
			}
		},
		methods: {
			selectlot() {
				this.$r.h(`/prod-api/api/park/lot/record/list?entryTime=${this.entryTime}&outTime=${this.outTime}`).then(
					res => {
						this.list = res.rows
					})
			},
			addpark() {
				this.temp = this.temp + 3
				this.$r.h(`/prod-api/api/park/lot/record/list?pageNum=0&pageSize=${this.temp}`).then(res => {
					this.list = res.rows
				})
			}
		},
		onLoad() {

			this.$r.h(`/prod-api/api/park/lot/record/list?pageNum=0&pageSize=${this.temp}`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>
