<template>
	<view>
		<image :src="$u.a+item.imgUrl" mode=""></image>
		<uni-section title="区域简介" sub-title="" type="line">
			<view>{{item.introduce}}</view>
		</uni-section>


		<uni-section title="人才政策文件列表" sub-title="" type="line">
			<uni-list v-for="(item,index) in list" :key="index">
				<navigator :url="`../policyDeatil/policyDeatil?id=${item.id}`">
					<uni-list-item :title="`标题:${item.title}\n日期:${item.createTime}`" note=""></uni-list-item>
				</navigator>
			</uni-list>

		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				item: [],
				list: []
			}
		},
		methods: {

		},
		onLoad(e) {
			this.$r.h(`/prod-api/api/youth-inn/talent-policy-area/` + e.id).then(res => {
				this.item = res.data
			})

			this.$r.h(`/prod-api/api/youth-inn/talent-policy/list?areaId=${e.id}`).then(res => {
				this.list = res.data
			})
		}
	}
</script>

<style>

</style>
