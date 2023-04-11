<template>
	<view>
		<image :src="$u.a+item.imgUrl" mode=""></image>

		<uni-section title="图书馆信息" sub-title="" type="line">
			<uni-list>
				<uni-list-item
					:title="`图书馆名称:${item.name}\n图书馆具体地址:${item.address}\n图书馆介绍:${item.description}\n营业时间:${item.businessHours}\n营业状态:${item.businessState=='1'?'营业中':'未营业'}\n`"
					note="">
				</uni-list-item>
			</uni-list>
		</uni-section>
		<navigator :url="`../commitDetail/commitDetail?id=${id}`"> <button type="primary" @click="commit">评论</button>
		</navigator>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				item: [],
				id: 0
			}
		},
		methods: {},
		onLoad(e) {
			this.id = e.id
			this.$r.h(`/prod-api/api/digital-library/library/${e.id}`).then(res => {
				this.item = res.data
			})
		}
	}
</script>

<style>

</style>
