<template>
	<view>
		<uni-forms ref="form" style="margin: 100rpx;">
			<uni-forms-item label="评分" name="">
				<uni-rate v-model="score"></uni-rate>
			</uni-forms-item>
			<uni-forms-item label="内容" name="">
				<textarea v-model="content" maxlength="150" style="width: 100%; border: 1px solid black;"></textarea>
				字数{{content.length}}/150
			</uni-forms-item>
			<button type="primary" style="margin: 50rpx;" @click="commit">评论</button>
		</uni-forms>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				score: "",
				content: "",
				id: 0
			}
		},
		methods: {
			commit() {
				this.$r.h(`/prod-api/api/lawyer-consultation/legal-advice/evaluate`, 'post', {
					"id": this.id,
					"evaluate": this.content,
					"score": this.score
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: res.msg
						});
					} else {
						uni.showToast({
							title: res.msg
						});
					}
				})
			}
		},
		onLoad(e) {
			this.id = e.id
		}
	}
</script>

<style>

</style>
