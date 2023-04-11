<template>
	<view>
		<view v-for="(item,index) in list.slice(0,5)" :key="index">
			<uni-list>
				<uni-list-item title="" note="">
					<template v-slot:body>

						<view style="display: flex;">
							<view>
								<view>快递单号:{{item.infoNo}}</view>
								<view>投诉内容:{{item.description}}</view>
								<view>投诉日期:{{item.createTime}}</view>
							</view>
						</view>
					</template>
				</uni-list-item>
			</uni-list>

		</view>
		<navigator style="height: 100%;" :url="`../AddOrder/AddOrder?id=${this.id}`"> <button type="primary">新增</button>
		</navigator>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [],
				id: 0
			}
		},
		methods: {

		},
		onLoad(e) {
			this.id = e.id
			this.$r.h(`/prod-api/api/logistics-inquiry/logistics_complaint/my-list`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>