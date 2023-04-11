<template>
	<view>
		<rich-text :nodes="item.content"></rich-text>

		<uni-section title="评论" sub-title="" type="line">
			<uni-forms-item label="内容" name="">
				<textarea v-model="contents" maxlength="150" style="width: 80%; border: 1px solid black;"></textarea>
				字数{{contents.length}}/150
			</uni-forms-item>
			<button type="primary" style="margin: 50rpx;" @click="subcommit">评论</button>
		</uni-section>

		<uni-section title="活动评论" sub-title="" type="line">
			<uni-list v-for="(item,index) in list.slice(0,5)" :key="index">
				<uni-list-item
					:title="`活动名:${item.activityName}\n用户名:${item.userName}\n评论内容:${item.content}\n评论时间:${item.commentTime}`"
					note=""></uni-list-item>
			</uni-list>
		</uni-section>


		<uni-section title="推荐活动" sub-title="" type="line">
			<view v-for="(item,index) in list2.slice(0,3)" :key="index">
				<uni-card>
					<!-- <navigator url="pages/Active" style="height: 100%;"> -->
					<view style="display: flex;">
						<view @click="shen(item.id)">
							<image :src="$u.a+item.imgUrl" style="width: 320rpx; height: 320rpx; margin-right: 20rpx;"
								mode=""></image>
						</view>
						<view>

							<view style="font-weight: bold;">{{item.name}}</view>
							<view>报名人数:{{item.signupNum}}</view>
							<view>点赞数:{{item.likeNum}}</view>
						</view>
					</view>
					<!-- </navigator> -->
				</uni-card>
			</view>
		</uni-section>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				item: [],
				list: [],
				contents: "",
				id: 0,
				list2: []
			}
		},
		methods: {
			subcommit(e) {
				this.$r.h(`/prod-api/api/activity/comment`, 'post', {
					'activityId': this.id,
					'content': this.contents
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: res.msg,
							success: () => {
								this.contents = ""
								this.$r.h(`/prod-api/api/activity/comment/list?activityId=${this.id}`)
									.then(res => {
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
			this.$r.h(`/prod-api/api/activity/activity/` + e.id).then(res => {
				this.item = res.data
			})

			this.$r.h(`/prod-api/api/activity/comment/list?activityId=${e.id}`).then(res => {
				this.list = res.rows
			})

			this.$r.h(`/prod-api/api/activity/activity/list?recommend=Y`).then(res => {
				this.list2 = res.rows
			})
		}
	}
</script>

<style>

</style>
