<template>
	<view>
		<uni-section title="医院列表" sub-title="" type="line">
			<view v-for="(item,index) in list" :key="index">
				<uni-list>
					<uni-list-item title="" note="">
						<template v-slot:body>
							<navigator
								:url="`../OutpatientAppointmentDeatil/OutpatientAppointmentDeatil?id=${item.id}&item=${JSON.stringify(item)}`">
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
				list: []
			}
		},
		methods: {

		},
		onLoad(e) {
			this.$r.h(`/prod-api/api/hospital/hospital/list?hospitalName=${e.id}`).then(res => {
				this.list = res.rows
			})
		}
	}
</script>

<style>

</style>
