<template>
	<view>
		<view style="width: 100%; display: flex;">
			<uni-search-bar style="width: 80%;" placeholder="请输入内容" @confirm="confirm"></uni-search-bar>
			<image @click="tosubway" src="../../static/volun/bus2.png"
				style="width: 20%; border-radius: 50%; height: 110rpx; line-height: 100rpx;" mode="">
			</image>
		</view>

		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,index) in sp" :key="index">
				<navigator :url="`newDetail/newDetail?id=${item.id}`" style="height: 100%;">
					<image :src="$u.a+item.advImg" style="width: 100%; height: 100%;"></image>
				</navigator>
			</swiper-item>
		</swiper>

		<uni-section title="应用服务入口" sub-title="" type="line">
			<uni-grid :column="5" :showBorder="false">
				<uni-grid-item v-for="(item,index) in icon.slice(0,9)" :key="index">
					<view class="imgs" @click="toservice(item.serviceName)">
						<image :src="$u.a+item.imgUrl" style="width: 80rpx; height: 80rpx; border-radius: 50%;" mode="">
						</image>
						<view>{{item.serviceName}}</view>
					</view>
				</uni-grid-item>
				<uni-grid-item>
					<view class="imgs" @click="toall">
						<image src="../../static/serviceicon/more.png"
							style="width: 80rpx; height: 80rpx; border-radius: 50%;" mode="">
						</image>
						<view>更多服务</view>
					</view>
				</uni-grid-item>
			</uni-grid>
		</uni-section>

		<uni-section title="热门主题" sub-title="" type="line">
			<uni-grid :column="2" :showBorder="false">
				<uni-grid-item v-for="(item,index) in hot" :key="index">
					<navigator :url="`newDetail/newDetail?id=${item.id}`">
						<view class="imgs">
							<image :src="$u.a+item.cover" style="width: 320rpx; height: 320rpx; border-radius: 20rpx;"
								mode="">
							</image>
							<view>{{item.title?item.title.slice(0,13)+'...':''}}</view>
						</view>
					</navigator>
				</uni-grid-item>
			</uni-grid>
		</uni-section>

		<uni-section title="新闻专栏" sub-title="" type="line">
			<uni-row>
				<uni-col :span="24/text.length" v-for="(item,index) in text" :key="index">
					<view @click="textc(item.id)" style="text-align: center;" :style="id==item.id?'color:blue':''">
						{{item.name}}
					</view>
				</uni-col>
			</uni-row>

			<view v-for="(item,index) in list" :key="index">
				<uni-card>
					<navigator :url="`newDetail/newDetail?id=${item.id}`" style="height: 100%;">
						<view style="display: flex;">
							<view>
								<image :src="$u.a+item.cover"
									style="width: 320rpx; height: 320rpx; margin-right: 20rpx;" mode=""></image>
							</view>
							<view>
								<view style="font-weight: bold;">{{item.title}}</view>
								<rich-text :nodes="item.content?item.content.slice(0,30)+'...':''"></rich-text>
								<view>评论总数:{{item.commentNum}}</view>
								<view>发布时间:{{item.publishDate}}</view>
							</view>
						</view>
					</navigator>
				</uni-card>
			</view>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				sp: [],
				icon: [],
				hot: [],
				text: [],
				list: [],
				id: 9
			}
		},

		methods: {
			tosubway() {
				uni.navigateTo({
					url: '/pages/citySubway/citySubwayImgage/citySubwayImgage'
				})
			},
			toservice(e) {
				if (e == "志愿服务") {
					uni.navigateTo({
						url: "/pages/Volunteerservice/Volunteerservice"
					});
					return;
				}
				
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
				uni.navigateTo({
					url: '/pages/index/serachList/serachList?id=' + e.value
				})
			},
			toall() {
				uni.switchTab({
					url: '/pages/two/two'
				})
			},
			textc(e) {
				this.id = e
				this.$r.h(`/prod-api/press/press/list?type=${e}`).then(res => {
					this.list = res.rows
				})
			}
		},
		onLoad() {
			this.textc(this.id)

			this.$r.h(`/prod-api/api/rotation/list`).then(res => {
				this.sp = res.rows
			})

			this.$r.h(`/prod-api/api/service/list`).then(res => {
				this.icon = res.rows
			})

			this.$r.h(`/prod-api/press/press/list?hot=Y`).then(res => {
				this.hot = res.rows
			})

			this.$r.h(`/prod-api/press/category/list`).then(res => {
				this.text = res.data
			})


		},
	}
</script>

<style>

</style>