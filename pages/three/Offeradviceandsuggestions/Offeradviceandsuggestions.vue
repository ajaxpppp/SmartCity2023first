<template>
	<view>
		<uni-section title="提交问题" sub-title="" type="line">
			<uni-forms ref="form" style="margin: 50rpx;">
				<uni-forms-item label="标题" name="">
					<uni-easyinput v-model="title" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="内容" name="">
					<textarea v-model="content" maxlength="150"
						style="width: 100%; border: 1px solid black;"></textarea>
					字数{{content.length}}/150
				</uni-forms-item>
				<button type="primary" style="margin: 50rpx;" @click="commit">提交</button>
			</uni-forms>
		</uni-section>

		<uni-section title="评论列表" sub-title="" type="line">
			<uni-list v-for="(item,index) in list" :key="index">
				<uni-list-item :title="`用户名:${item.user}\n内容:${item.content}`" note=""></uni-list-item>
			</uni-list>
		</uni-section>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: "",
				content: "",
				list: [{
					user: "小张",
					content: "永远跟党走"
				}, {
					user: "小王",
					content: "永远跟党走"
				}, {
					user: "小丽",
					content: "永远跟党走"
				}]
			}
		},
		methods: {
			commit() {
				uni.showToast({
					title: '提交成功'
				});
				let user = this.title
				let content = this.content
				this.list.unshift({
					user: user,
					content: content
				})
				this.title=""
				this.content=""
			}
		}
	}
</script>

<style>

</style>