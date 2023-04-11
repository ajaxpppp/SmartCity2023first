<template>
	<view>
		<uni-section title="宠物种类" sub-title="" type="line">
			<uni-grid :column="5" :showBorder="false">
				<uni-grid-item v-for="(item,index) in icon" :key="index">
					<navigator :url="`FindAdoctor/FindAdoctor?id=${item.id}`">
						<view class="imgs">
							<image style="width: 80rpx; height: 80rpx;" :src="$u.a+item.imgUrl" mode=""></image>
							<view>{{item.name}}</view>
						</view>
					</navigator>
				</uni-grid-item>
			</uni-grid>
		</uni-section>

		<view style="height: 20rpx;"></view>
		<uni-section title="我的问诊列表" sub-title="" type="line">
			<view v-for="(item,index) in list.slice(0,5)" :key="index" v-if="item.doctor">
				<uni-list>
					<uni-list-item title="" note="">
						<template v-slot:body>
							<navigator
								:url="`ConsultationDetailsPage/ConsultationDetailsPage?id=${JSON.stringify(item)}`">
								<view style="display: flex;">
									<view>
										<image
											style="width: 320rpx; height: 220rpx; border-radius: 20rpx; margin-right: 20rpx;"
											:src="$u.a+item.doctor.avatar" mode=""></image>
									</view>
									<view>
										<view style="font-weight: bold;">医生姓名:{{item.doctor.name}}</view>
										<view>案例描述:{{item.question}}</view>
									</view>
								</view>
							</navigator>
						</template>
					</uni-list-item>
				</uni-list>
			</view>
		</uni-section>

		<view style="height: 20rpx;"></view>
		<uni-section title="问诊案例列表" sub-title="" type="line">
			<view v-for="(item,index) in list2" :key="index" v-if="item.doctor">
				<uni-list>
					<uni-list-item title="" note="">
						<template v-slot:body>
							<navigator :url="`CaseDetailsPage/CaseDetailsPage?id=${JSON.stringify(item)}`">
								<view style="display: flex;">
									<view>
										<image
											style="width: 320rpx; height: 220rpx; border-radius: 20rpx; margin-right: 20rpx;"
											:src="$u.a+item.doctor.avatar" mode=""></image>
									</view>
									<view>
										<view style="font-weight: bold;">医生姓名:{{item.doctor.name}}</view>
										<view>案例描述:{{item.question}}</view>
									</view>
								</view>
							</navigator>
						</template>
					</uni-list-item>
				</uni-list>
			</view>


		</uni-section>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				icon: [],
				list: [],
				list2: []
			}
		},
		methods: {

		},
		onLoad() {
			this.$r.h(`/prod-api/api/pet-hospital/pet-type/list`).then(res => {
				this.icon = res.data
			})

			this.$r.h(`/prod-api/api/pet-hospital/inquiry/my-list`).then(res => {
				this.list = res.rows
			})

			this.$r.h(`/prod-api/api/pet-hospital/inquiry/list?pageNum=0&pageSize=10`).then(res => {
				this.list2 = res.rows
			})
		}
	}
</script>

<style>

</style>