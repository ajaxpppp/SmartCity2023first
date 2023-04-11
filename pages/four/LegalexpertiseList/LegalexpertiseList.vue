<template>
	<view>
		<uni-section title="律师列表" sub-title="" type="line">
			<view style="display: flex; width: 100%;">
				<uni-data-select style="width: 80%; margin-left: 40rpx;" @change="change" :localdata="location"
					v-model="value">
				</uni-data-select>
				<button type="primary" size="mini" style="width: 20%;" @click="clicklist">筛选</button>
			</view>
			<view v-for="(item,index) in list" :key="index">
				<uni-card>

					<view style="display: flex;">
						<view>
							<image :src="$u.a+item.avatarUrl"
								style="width: 320rpx; height: 320rpx; margin-right: 20rpx;" mode=""></image>
						</view>
						<view>
							<view style="font-weight: bold;">{{item.name}}</view>
							<view>从业年限:{{item.workStartAt}}年</view>
							<view>咨询人数:{{item.serviceTimes}}人</view>
							<view>法律专长:{{item.legalExpertiseName}}</view>
							<view>好评率:{{item.favorableRate}}%</view>
							<navigator :url="`../LegalexpertiseDetail/LegalexpertiseDetail?id=${item.id}`"
								style="height: 100%;"> <button type="primary" size="mini">咨询</button></navigator>
						</view>
					</view>

				</uni-card>
			</view>
		</uni-section>


		<uni-popup ref="popup" type="center">
			<uni-popup-message v-if="temp==true">
				<uni-section title="全部法律专长列表" sub-title="" type="line">
					<scroll-view scroll-y="true" style="width:720rpx; height: 600rpx;">
						<uni-grid :column="4" :showBorder="false">
							<uni-grid-item v-for="(item,index) in icon" :key="index" style="width: 25%;">
								<view @click="selectService(item.id)" class="imgs" style="font-size: 18rpx;">
									<image style="width: 80rpx; height: 80rpx; border-radius: 50%;"
										:src="$u.a+item.imgUrl" mode=""></image>
									<view>{{item.name}}</view>
								</view>
							</uni-grid-item>
						</uni-grid>
					</scroll-view>
				</uni-section>
			</uni-popup-message>
		</uni-popup>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [],
				temp: false,
				value: "0",
				location: [{
					text: "默认排序",
					value: "0"
				}, {
					text: "从业年限",
					value: "workStartAt"
				}, {
					text: "服务人数",
					value: "serviceTimes"
				}, {
					text: "好评率",
					value: "favorableRate"
				}],
				icon: []
			}
		},
		methods: {
			clicklist() {
				this.$refs.popup.open()
				this.temp = true
			},
			selectService(e) {
				this.$r.h(`/prod-api/api/lawyer-consultation/lawyer/list?legalExpertiseId=${e}`).then(res => {
					this.list = res.rows
					let date = new Date()
					for (let s of this.list) {
						s.workStartAt = parseInt(date.getFullYear()) - parseInt(s.workStartAt.slice(0, 4))
					}
					this.temp = false
				})
			},
			change(e) {
				this.$r.h(`/prod-api/api/lawyer-consultation/lawyer/list?sort=${e}`).then(res => {
					this.list = res.rows
					let date = new Date()
					for (let s of this.list) {
						s.workStartAt = parseInt(date.getFullYear()) - parseInt(s.workStartAt.slice(0, 4))
					}
				})
			}
		},
		onLoad(e) {
			if (e.id != null) {
				this.$r.h(`/prod-api/api/lawyer-consultation/lawyer/list?legalExpertiseId=${e.id}`).then(res => {
					this.list = res.rows
					let date = new Date()
					for (let s of this.list) {
						s.workStartAt = parseInt(date.getFullYear()) - parseInt(s.workStartAt.slice(0, 4))
					}
				})
			} else {
				this.$r.h(`/prod-api/api/lawyer-consultation/lawyer/list`).then(res => {
					this.list = res.rows
					let date = new Date()
					for (let s of this.list) {
						s.workStartAt = parseInt(date.getFullYear()) - parseInt(s.workStartAt.slice(0, 4))
					}
				})
			}


			this.$r.h(`/prod-api/api/lawyer-consultation/legal-expertise/list`).then(res => {
				this.icon = res.rows.sort(function(a, b) {
					return b.sort - a.sort
				})

			})
		}
	}
</script>

<style>

</style>
