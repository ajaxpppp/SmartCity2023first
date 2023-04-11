<template>
	<view>
		<view class="title">{{item.title}}</view>
		<rich-text :nodes="item.content"></rich-text>
		<view style="text-align: right;">
			<view>发布人:{{item.author}}</view>
			<view>{{item.createTime}}</view>
		</view>

		<uni-section title="匿名评论" sub-title="" type="line">
			<uni-forms style="padding: 50rpx;" ref="form">
				<uni-forms-item label="正文" name="">
					<textarea maxlength="30" v-model="password" style="border: 1px solid; width: 100%;"
						placeholder="" />
					字数:{{password.length}}
				</uni-forms-item>
				<button type="primary" style="margin: 50rpx;" @click="login">评论</button>
			</uni-forms>
		</uni-section>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				item: [],
				password: "",
				id: ''
			}
		},
		methods: {
			login() {
				this.$r.h(`/prod-api/api/garbage-classification/news-comment`, 'post', {
					"newsId": this.id,
					"content": this.password
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: res.msg
						});
						this.password = ""
					}
				})
			}
		},
		onLoad(e) {
			this.id = e.id
			this.$r.h(`/prod-api/api/garbage-classification/news/` + e.id).then(res => {
				this.item = res.data
			})
		}
	}
</script>

<style>

</style>
