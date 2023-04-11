<template>
	<view>
		<uni-search-bar @confirm="confirm" @input="" placeholder="请输入医院名称" />
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,index) in sp" :key="index">
				<navigator
					:url="`OutpatientAppointmentDeatil/OutpatientAppointmentDeatil?id=${item.id}&item=${JSON.stringify(item)}`"
					style="height: 100%;">
					<image :src="$u.a+item.imgUrl" style="height: 100%;" mode=""></image>
				</navigator>
			</swiper-item>
		</swiper>

		<uni-section title="医院列表" sub-title="" type="line">
			<view v-for="(item,index) in list" :key="index">
				<uni-list>
					<uni-list-item title="" note="">
						<template v-slot:body>
							<navigator
								:url="`OutpatientAppointmentDeatil/OutpatientAppointmentDeatil?id=${item.id}&item=${JSON.stringify(item)}`">
								<view style="display: flex;">
									<view>
										<image
											style="width: 320rpx; height: 220rpx; border-radius: 10rpx; margin-right: 20rpx;"
											:src="$u.a+item.imgUrl" mode=""></image>
									</view>
									<view>
										<view class="text3">
											<rich-text :nodes="item.brief?item.brief.slice(0,50)+'...':''"></rich-text>
										</view>
										<uni-rate :value="item.level"></uni-rate>
									</view>
								</view>
							</navigator>
						</template>
					</uni-list-item>
				</uni-list>
			</view>
		</uni-section>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				sp: [],
				list: []
			}
		},
		methods: {
			confirm(e) {
				uni.navigateTo({
					url: '/pages/OutpatientAppointment/serachHospital/serachHospital?id=' + e.value,
				});
			}
		},
		onLoad() {
			this.$r.h(`/prod-api/api/hospital/banner/list`).then(res => {
				this.sp = res.data
			})

			this.$r.h(`/prod-api/api/hospital/hospital/list`).then(res => {
				this.list = res.rows
			})


		}
	}
</script>

<style>

</style>
