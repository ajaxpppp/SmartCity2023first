<template>
	<view>
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,index) in sp" :key="index">
				<image @click="tonewdetials(item.id)" :src="$u.a+item.advImg" style="width: 100%; height: 100%;">
				</image>
			</swiper-item>
		</swiper>

		<uni-search-bar @confirm="confirm" placeholder="搜索" />

		<uni-section title="热门职位" sub-title="" type="line">
			<uni-grid :column="3" :showBorder="false">
				<uni-grid-item v-for="(item,index) in grids.slice(0,9)" :key="index">
					<navigator :url="`job-huntingDetail/job-huntingDetail?id=${item.id}`" style="height: 100%;">
						<view
							style=" height: 100%;  display: flex;flex-direction: column; justify-content: center; align-items: center;">
							{{item.professionName}}
						</view>
					</navigator>
				</uni-grid-item>
			</uni-grid>
		</uni-section>

		<uni-section title="所有职位" sub-title="" type="line">
			<view v-for="(item,index) in  grids" :key="index">
				<navigator :url="`job-huntingDetail/job-huntingDetail?id=${item.id}`">
					<uni-list>
						<uni-list-item :title="item.professionName" note=""></uni-list-item>
					</uni-list>
				</navigator>
			</view>
		</uni-section>


	</view>
</template>

<script>
	export default {
		data() {
			return {
				sp: [],
				grids: []
			}
		},
		methods: {
			confirm(e) {
				this.$r.h(`/prod-api/api/job/profession/list?professionName=${e.value}`).then(res => {
					this.grids = res.rows
				})
			},
		},
		onLoad() {
			this.$r.h(`/prod-api/api/rotation/list`).then(res => {
				this.sp = res.rows
			})

			this.$r.h(`/prod-api/api/job/profession/list`).then(res => {
				this.grids = res.rows
			})
		}
	}
</script>

<style>

</style>