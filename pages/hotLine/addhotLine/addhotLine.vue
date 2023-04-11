<template>
	<view>

		<uni-forms ref="form" style="padding: 80rpx;">
			<uni-forms-item label="述求分类" name="" v-if="temp==23">
				<uni-data-select :localdata="localdata" v-model="value">
				</uni-data-select>
			</uni-forms-item>
			<uni-forms-item label="标题" name="">
				<uni-easyinput v-model="title" placeholder="" />
			</uni-forms-item>
			<uni-forms-item label="述求内容" name="">
				<uni-easyinput v-model="content" placeholder="" />
			</uni-forms-item>
			<uni-forms-item label="图片" name="">
				<image @click="img" :src="$u.a+`/prod-api/`+imgUrl"
					style="width:450rpx; height: 400rpx; border: 1px solid; " mode="">
				</image>
			</uni-forms-item>
			<uni-forms-item label="承办单位" name="">
				<uni-easyinput v-model="undertaker" placeholder="" />
			</uni-forms-item>
			<uni-forms-item label="反馈手机号" name="">
				<uni-easyinput v-model="phonenumber" placeholder="" />
			</uni-forms-item>
			<button type="primary" @click="ccc">发布</button>
		</uni-forms>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				temp: 0,
				localdata: [],
				value: '',
				user: [],
				"appealCategoryId": 0,
				"title": "",
				"content": "",
				"undertaker": "",
				"imgUrl": "",
				id: 0,
				phonenumber: ""
			}
		},
		methods: {
			ccc() {
				this.$r.h(`/prod-api/api/gov-service-hotline/appeal`, 'post', {
					"appealCategoryId": this.value || this.id,
					"title": this.title,
					"content": this.content,
					"undertaker": this.undertaker,
					"imgUrl": this.imgUrl,
				}).then(res => {
					if (res.code == 200) {
						uni.showToast({
							title: res.msg
						});
						this.title = ""
						this.content = ""
						this.undertaker = ""
						this.imgUrl = ""
						this.phonenumber = ""
						this.value = ""
					}
				})
			},
			img() {
				uni.chooseImage({
					count: 1,
					success: (res) => {
						uni.uploadFile({
							url: this.$u.a + "/prod-api/common/upload",
							method: 'post',
							name: "file",
							header: {
								Authorization: uni.getStorageSync("token")
							},
							filePath: res.tempFilePaths[0],
							success: res => {
								let iamges = JSON.parse(res.data)
								this.imgUrl = iamges.fileName
							}
						})
					}
				})
			}
		},
		onLoad(e) {
			this.id = e.id
			this.temp = e.temp
			this.$r.h(`/prod-api/api/gov-service-hotline/appeal-category/list`).then(res => {
				for (let s of res.rows) {
					let value = s.id
					let text = s.name
					this.localdata.push({
						value,
						text
					})
				}
			})
		}
	}
</script>

<style>

</style>
