<template>
	<view>
		<uni-forms ref="form" style="margin: 100rpx;">
			<uni-forms-item label="标题" name="">
				<uni-easyinput v-model="title" placeholder="" />
			</uni-forms-item>
			<uni-forms-item label="内容" name="">
				<textarea v-model="content" maxlength="150" style="width: 100%; border: 1px solid black;"></textarea>
				字数{{content.length}}/150
			</uni-forms-item>
			<button type="primary" style="margin: 50rpx;" @click="commit">评论</button>
		</uni-forms>

		<uni-section title="评论列表" sub-title="" type="line">
			<view v-for="(item,index) in list.slice(0,5)" :key="index" style="margin: 50rpx;">
				<view>用户Id:{{item.userId}}</view>
				<view>评论标题:{{item.title}}</view>
				<view>评论内容:{{item.content}}</view>
			</view>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: "",
				content: "",
				list: []
			}
		},
		methods: {
			commit() {
				this.$r.h(`/prod-api/api/common/feedback`, 'post', {
					"content": this.content,
					"title": this.title
				}).then(res => {
					if (res.code == 200) {
						this.title = ""
						this.content = ""
						uni.showToast({
							title: res.msg
						});
						this.$r.h(`/prod-api/api/common/feedback/list`).then(res => {
							this.list = res.rows
						})
					}
				})
			}
		},
		onLoad() {
			this.$r.h(`/prod-api/api/common/feedback/list`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>
