<template>
	<view>
		<uni-section title="医生列表" sub-title="" type="line">
			<view v-for="(item,index) in list" :key="index">
				<uni-list>
					<uni-list-item title="" note="">
						<template v-slot:body>
							<navigator :url="`../Consultationpage/Consultationpage?id=${JSON.stringify(item)}`">
								<view style="display: flex;">
									<view>
										<image
											style="width: 320rpx; height: 220rpx; border-radius: 20rpx; margin-right: 20rpx;"
											:src="$u.a+item.avatar" mode=""></image>
									</view>
									<view>
										<view style="font-weight: bold;">医生姓名:{{item.name}}</view>
										<view>职称:{{item.jobName}}</view>
										<view>职业编号:{{item.practiceNo}}</view>
										<view>从业年限:{{item.workingYears}}</view>
									</view>
								</view>
							</navigator>
						</template>
					</uni-list-item>

				</uni-list>
				<view>擅长描述:{{item.goodAt}}</view>
			</view>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [],

			}
		},
		methods: {

		},
		onLoad(e) {
			this.$r.h(`/prod-api/api/pet-hospital/pet-doctor/list?typeId=` + e.id).then(res => {
				this.list = res.rows
				console.log(this.list);
			})
		}
	}
</script>

<style>

</style>