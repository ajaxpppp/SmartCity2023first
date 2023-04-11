<template>
	<view>
		<view class="title">{{item.title}}</view>
		<image :src="item.url" mode=""></image>
		<view>{{item.content}}</view>

		<uni-section title="文字评论" sub-title="" type="line" v-if="temp==true">
			<uni-forms ref="form" style="margin: 50rpx;">
				<uni-forms-item label="标题" name="">
					<uni-easyinput v-model="title" placeholder="" />
				</uni-forms-item>
				<uni-forms-item label="内容" name="">
					<textarea v-model="content" maxlength="150"
						style="width: 100%; border: 1px solid black;"></textarea>
					字数{{content.length}}/150
				</uni-forms-item>
				<button type="primary" style="margin: 50rpx;" @click="commit">评论</button>
			</uni-forms>
		</uni-section>

		<view v-if="num==1">
			<button type="primary" @click="add">活动报名</button>
			<uni-section title="活动留言" sub-title="" type="line">
				<uni-forms ref="form" style="margin: 50rpx;">
					<uni-forms-item label="标题" name="">
						<uni-easyinput v-model="title" placeholder="" />
					</uni-forms-item>
					<uni-forms-item label="内容" name="">
						<textarea v-model="content" maxlength="150"
							style="width: 100%; border: 1px solid black;"></textarea>
						字数{{content.length}}/150
					</uni-forms-item>
					<button type="primary" style="margin: 50rpx;" @click="liu">留言</button>
				</uni-forms>
			</uni-section>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				num: 0,
				item: [],
				title: "",
				temp: false,
				content: "",
			}
		},
		methods: {
			liu(){
				uni.showToast({
					title: '留言成功'
				});
				this.title = ""
				this.content = ""
			},
			add() {
				uni.showToast({
					title: '报名成功'
				});
			},
			commit() {
				uni.showToast({
					title: '评论成功'
				});
				this.title = ""
				this.content = ""
			}

		},
		onLoad(e) {
			this.item = JSON.parse(e.id)
			this.num = JSON.parse(e.num)
			this.temp = JSON.parse(e.temp)
		}
	}
</script>

<style>

</style>