<template>
	<view>
		<view>
			<view>
				<uni-section :title="item.name" sub-title="" type="line">
					<view style="display: flex;">
						<image style="width: 1500rpx;" :src="$u.a+item.imgUrl" mode=""></image>
						<view>
							<uni-section title="分类说明" sub-title="" type="line">
								{{item.guide}}
							</uni-section>
						</view>
					</view>
					<uni-section title="分类介绍" sub-title="" type="circle">
						<view>{{item.introduce}}</view>
					</uni-section>
				</uni-section>
			</view>

		</view>
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
			this.$r.h(`/prod-api/api/garbage-classification/garbage-classification/list`).then(res => {
				for (let s of res.rows) {
					if (e.id == s.id) {
						this.item = s
						break;
					}
				}

			})
		}
	}
</script>

<style>

</style>
