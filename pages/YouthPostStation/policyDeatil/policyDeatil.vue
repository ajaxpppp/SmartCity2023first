<template>
	<view>
		<uni-section title="人才政策文件" sub-title="" type="line">
			<uni-list>

				<uni-list-item :title="`标题:${item.title}\n日期:${item.createTime}\n发布者:${item.author}`" note="">
				</uni-list-item>
				<rich-text :nodes="item.content"></rich-text>
			</uni-list>

		</uni-section>
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
			this.$r.h(`/prod-api/api/youth-inn/talent-policy/` + e.id).then(res => {
				this.item = res.data
			})
		}
	}
</script>

<style>

</style>
