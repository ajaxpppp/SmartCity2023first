<template>
	<view style="width: 100%;">
		<uni-search-bar placeholder="请输入服务名称" @confirm="confirm"></uni-search-bar>

		<view style="display: flex;">
			<view style="width: 20%;">
				<view v-for="(item,index) in serivceType" style="width:100%; height: 120rpx; border: 1px solid Gray; "
					:key="index">
					<view :style="item==value?'color:blue':''" @click="textc(item)"
						style="position: relative; top: 30%; text-align: center;  height: 100% ;width: 100%;">
						{{item}}
					</view>
				</view>
			</view>

			<view style="width: 80%;">
				<view style="width: 100%; height: 100%; border: 1px solid beige;">
					<uni-grid :column="3" :showBorder="false">
						<uni-grid-item v-for="(item,index) in icon" :key="index">
							<view v-if="'律师咨询'!=item.serviceName" class="imgs" @click="toservice(item.serviceName)">
								<image :src="$u.a+item.imgUrl" style=" width: 80rpx; height: 80rpx; border-radius: 50%;"
									mode="">
								</image>
								<view>{{item.serviceName}}</view>
							</view>
							<view v-else class="imgs" @click="toservice(item.serviceName)">
								<image src="../../static/lawyer/lawyer.jpg"
									style=" width: 80rpx; height: 80rpx; border-radius: 50%;" mode=""></image>
								<view>{{item.serviceName}}</view>
							</view>
						</uni-grid-item>
					</uni-grid>
				</view>
			</view>

			<uni-popup ref="popup" type="center">
				<view style="width:100%; height: 100%;">
					<uni-popup-dialog>
						<uni-grid :column="4" :showBorder="false">
							<uni-grid-item v-for="(item,index) in icon2" :key="index">
								<view class="imgs" @click="toservice(item.serviceName)">
									<image :src="$u.a+item.imgUrl"
										style="width: 80rpx; height: 80rpx; border-radius: 50%;" mode="">
									</image>
									<view>{{item.serviceName}}</view>
								</view>
							</uni-grid-item>
						</uni-grid>
					</uni-popup-dialog>
				</view>
			</uni-popup>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				icon: [{}],
				icon2: [],
				value: "生活服务",
				serivceType: ['生活服务', '便民服务', '车主服务'],
				lawyer: [],
			}
		},
		methods: {
			toservice(e) {
				if (e == "停哪儿") {
					uni.navigateTo({
						url: '/pages/park/park'
					});
					return;
				}

				if (e == "数字图书馆") {
					uni.navigateTo({
						url: '/pages/VRlibrary/VRlibrary'
					});
					return;
				}

				if (e == "青年驿站") {
					uni.navigateTo({
						url: '/pages/YouthPostStation/YouthPostStation'
					});
					return;
				}

				if (e == "活动管理") {
					uni.navigateTo({
						url: '/pages/Active/Active'
					});
					return;
				}

				if (e == "智慧巴士") {
					uni.navigateTo({
						url: '/pages/smartBus/smartBus'
					});
					return;
				}

				if (e == "爱心捐赠") {
					uni.navigateTo({
						url: '/pages/loveDonation/loveDonation'
					});
					return;
				}

				if (e == "政府服务热线") {
					uni.navigateTo({
						url: '/pages/hotLine/hotLine'
					});
					return;
				}

				if (e == "数据分析") {
					uni.navigateTo({
						url: '/pages/DataAnalyse/DataAnalyse'
					});
					return;
				}

				if (e == "城市地铁") {
					uni.navigateTo({
						url: '/pages/citySubway/citySubway'
					});
					return;
				}

				if (e == "生活缴费") {
					uni.navigateTo({
						url: '/pages/lifePay/lifePay'
					});
					return;
				}

				if (e == "看电影") {
					uni.navigateTo({
						url: '/pages/watchMovie/watchMovie'
					});
					return;
				}

				if (e == "宠物医院") {
					uni.navigateTo({
						url: '/pages/petHospital/petHospital'
					});
					return;
				}

				if (e == "教育") {
					uni.navigateTo({
						url: '/pages/education/education'
					});
					return;
				}

				if (e == "垃圾分类") {
					uni.navigateTo({
						url: '/pages/refuseClassification/refuseClassification'
					});
					return;
				}

				if (e == "门诊预约") {
					uni.navigateTo({
						url: '/pages/OutpatientAppointment/OutpatientAppointment'
					});
					return;
				}

				if (e == "外卖订餐") {
					uni.navigateTo({
						url: '/pages/TakeOutorder/TakeOutorder'
					});
					return;
				}

				if (e == "找房子") {
					uni.navigateTo({
						url: '/pages/tohuntahouse/tohuntahouse'
					});
					return;
				}

				if (e == "找工作") {
					uni.navigateTo({
						url: '/pages/job-hunting/job-hunting'
					});
					return;
				}

				if (e == "物流查询") {
					uni.navigateTo({
						url: '/pages/LogisticsQuery/LogisticsQuery'
					});
					return;
				}

				if (e == "智慧交管") {
					uni.navigateTo({
						url: '/pages/Intelligenttrafficmanagement/Intelligenttrafficmanagement'
					});
					return;
				}

				if (e == "志愿服务") {
					uni.navigateTo({
						url: "/pages/Volunteerservice/Volunteerservice"
					});
					return;
				}

			},
			confirm(e) {
				this.$refs.popup.open()
				this.$r.h(`/prod-api/api/service/list?serviceName=${e.value}`).then(res => {
					this.icon2 = res.rows
				})
			},
			textc(e) {
				this.value = e
				this.$r.h(`/prod-api/api/service/list?serviceType=${e}`).then(res => {
					this.icon = res.rows
				})
			}
		},
		onLoad() {
			this.textc(this.value)
		}
	}
</script>

<style>

</style>