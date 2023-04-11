<template>
	<view>
		<uni-nav-bar right-icon="list" @clickRight="selectlist"></uni-nav-bar>
		<uni-section title="所有停车场" sub-title="" type="line">
			<uni-list v-for="(item,index) in list" :key="index">
				<navigator :url="`parkDeatil/parkDeatil?id=${item.id}`">
					<uni-list-item
						:title="`停车场名:${item.parkName}\n空位数量:${item.vacancy}个\n地址:${item.address}\n收费价格:${item.rates}元/小时\n距离:${item.distance}米`"
						note="">
					</uni-list-item>
				</navigator>
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
				temp: 6
			}
		},
		methods: {
			selectlist() {
				uni.navigateTo({
					url: 'parkList/parkList',
				});
			},
			addpark() {
				this.temp = this.temp + 3
				this.$r.h(`/prod-api/api/park/lot/list?pageNum=0&pageSize=${this.temp}`).then(res => {
					this.list = res.rows
				})
				console.log("this.temp: " + JSON.stringify(this.temp));
			}
		},
		onLoad() {
			this.$r.h(`/prod-api/api/park/lot/list?pageNum=0&pageSize=5`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>
