<template>
	<view>
		<uni-section title="图书馆列表" sub-title="" type="line">
			<uni-list v-for="(item,index) in list" :key="index">
				<navigator :url="`bookDetail/bookDetail?id=${item.id}`">
					<uni-list-item
						:title="`图书馆名称:${item.name}\n图书馆地址:${item.address}\n营业时间:${item.businessHours}\n营业状态:${item.businessState=='1'?'营业中':'未营业'}`"
						note="">
					</uni-list-item>
				</navigator>
			</uni-list>

		</uni-section>
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
		onLoad() {
			this.$r.h(`/prod-api/api/digital-library/library/list`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>
