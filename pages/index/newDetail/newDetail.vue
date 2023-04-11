<template>
	<view>
		<view class="title">{{item.title}}</view>
		<image :src="$u.a+item.cover">
		</image>
		<rich-text :nodes="item.content"></rich-text>

		<!-- <view style="display: flex; bottom:0; position: fixed;  width: 100%;  border: 1px solid red;">
			<uni-easyinput placeholder="请输入评论内容" v-model="contents"></uni-easyinput>
			<button type="primary" size="mini" @click="subcommit">评论</button>
		</view> -->
		<uni-forms ref="form" style="margin: 100rpx;">
			<!-- <uni-forms-item label="标题" name="">
				<uni-easyinput v-model="title" placeholder="" />
			</uni-forms-item> -->
			<uni-forms-item label="内容" name="">
				<textarea v-model="contents" maxlength="150" style="width: 100%; border: 1px solid black;"></textarea>
				字数{{contents.length}}/150
			</uni-forms-item>
			<button type="primary" style="margin: 50rpx;" @click="subcommit">评论</button>
		</uni-forms>

		<uni-section title="评论列表" sub-title="" type="line">
			<view v-for="(item,index) in list.slice(0,10)" :key="index" style="margin: 50rpx;">
				<view>用户名:{{item.userName}}</view>
				<view>评论内容:{{item.content}}</view>
				<view>评论时间:{{item.commentDate}}</view>
			</view>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				item: [],
				contents: "",
				list: [],
				id: null
			}
		},
		methods: {
			subcommit(e) {
				this.$r.h(`/prod-api/press/pressComment`, 'post', {
					'newsId': this.id,
					'content': this.contents
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: res.msg,
							success: () => {
								this.contents = ""
								this.$r.h(`/prod-api/press/comments/list?newsId=${this.id}`).then(
									res => {
										this.list = res.rows.sort(function(a, b) {
											return new Date(b.commentDate).getTime() -
												new Date(a.commentDate).getTime()
										})
									})

							}
						});
					}
				})
			}
		},
		onLoad(e) {
			this.id = e.id
			this.$r.h(`/prod-api/press/press/${e.id}`).then(res => {
				this.item = res.data
			})

			this.$r.h(`/prod-api/press/comments/list?newsId=${e.id}`).then(res => {
				this.list = res.rows.sort(function(a, b) {
					return new Date(b.commentDate).getTime() -
						new Date(a.commentDate).getTime()
				})
			})
		}
	}
</script>

<style>

</style>
