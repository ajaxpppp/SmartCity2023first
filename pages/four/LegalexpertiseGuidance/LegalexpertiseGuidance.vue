<template>
	<view>
		<view>
			<uni-section title="筛选列表" sub-title="" type="line">
				<uni-data-select style="width: 100%; padding: 30rpx;" @change="change" :localdata="location"
					v-model="value">
				</uni-data-select>
			</uni-section>


			<uni-section title="咨询列表" sub-title="" type="line">
				<view v-for="(item,index) in list" :key="index">
					<uni-card>
						<navigator
							:url="`../LegalexpertiseGuidanceDeatil/LegalexpertiseGuidanceDeatil?id=${JSON.stringify(item)}`"
							style="height: 100%;">
							<view style="display: flex;">
								<view>
									<image :src="$u.a+item.avatarUrl"
										style="width: 320rpx; height: 320rpx; margin-right: 20rpx;" mode=""></image>
								</view>
								<view>
									<view style="font-weight: bold;">{{item.name}}</view>
									<view>法律专长:{{item.legalExpertiseName}}</view>
									<view>受理状态:{{item.state==1?"已处理":"未处理"}}</view>
									<view>提交时间:{{item.createTime}}</view>
								</view>
							</view>
						</navigator>
					</uni-card>
				</view>
			</uni-section>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				value: "0",
				list: [],
				listc: [],
				location: [{
					text: "未处理",
					value: "0"
				}, {
					text: "已处理",
					value: "1"
				}],
			}
		},
		methods: {
			change(e) {
				this.value = e
				this.$r.h(`/prod-api/api/lawyer-consultation/legal-advice/list?state=${e}`).then(res => {
					this.list = res.rows.sort(function(a, b) {
						return b.createTime > a.createTime ? 1 : -1
					})
					for (let s of this.list) {
						this.$r.h(`/prod-api/api/lawyer-consultation/lawyer/${s.lawyerId}`).then(res => {
							s.avatarUrl = res.data.avatarUrl
							s.name = res.data.name
							s.legalExpertiseName = res.data.legalExpertiseName
							s.workStartAt = res.data.workStartAt
							s.serviceTimes = res.data.serviceTimes
							s.favorableRate = res.data.favorableRate
						})
					}
				})
			}
		},
		onLoad() {
			this.$r.h(`/prod-api/api/lawyer-consultation/legal-advice/list`).then(res => {
				this.list = res.rows.sort(function(a, b) {
					return b.createTime > a.createTime ? 1 : -1
				})
				for (let s of this.list) {
					this.$r.h(`/prod-api/api/lawyer-consultation/lawyer/${s.lawyerId}`).then(res => {
						s.avatarUrl = res.data.avatarUrl
						s.name = res.data.name
						s.legalExpertiseName = res.data.legalExpertiseName
						s.workStartAt = res.data.workStartAt
						s.serviceTimes = res.data.serviceTimes
						s.favorableRate = res.data.favorableRate
					})
				}
			})
		}
	}
</script>

<style>

</style>