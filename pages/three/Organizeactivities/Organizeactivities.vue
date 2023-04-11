<template>
	<view>
		<uni-section title="活动展示" sub-title="" type="line">
			<view v-for="(item,index) in list.slice(0,3)" :key="index">
				<uni-card>
					<navigator :url="`../Deatil/Deatil?id=${JSON.stringify(item)}&num=${1}`" style="height: 100%;">
						<view style="display: flex;">
							<view>
								<image :src="item.url" style="width: 320rpx; height: 320rpx; margin-right: 20rpx;"
									mode=""></image>
							</view>
							<view>
								<view style="font-weight: bold;">{{item.title}}</view>
								<rich-text :nodes="item.content?item.content.slice(0,30)+'...':''"></rich-text>
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
				current: 0,
				text: ['2021年', '2022年', '2023年'],
				list: [{
					url: '/static/partyBuilding/(27).jpg',
					title: '中国建筑标准设计研究院党建云',
					content: '为进一步加强党务共建与政企交流，深入创新党建工作,2020年12月21日，温州机场集团机关直属第一党支部、第二党支部与国航股份有限公司温州分公司机关党支部共同参加了由浙江省空港贵宾服务有限公司第四党支部牵头组织的赴正泰集团开展党务共建暨主题党日活动。',
					id: 0
				}, {
					url: '/static/partyBuilding/(28).jpg',
					title: '中国物流股份有限公司党建云',
					content: '为进一步加强党务共建与政企交流，深入创新党建工作,2020年12月21日，温州机场集团机关直属第一党支部、第二党支部与国航股份有限公司温州分公司机关党支部共同参加了由浙江省空港贵宾服务有限公司第四党支部牵头组织的赴正泰集团开展党务共建暨主题党日活动。',
					id: 2
				}, {
					url: '/static/partyBuilding/(29).jpg',
					title: '中国建筑标准设计研究院党建云',
					content: '　为贯彻落实习近平总书记加强国有企业境外单位党的建设要求，为30余家驻摩洛哥中资企业、机构建立一个党建平台，将党建工作纳入统一管理，成为加强海外党建工作的有力抓手，2018年5月，在中国驻摩洛哥使馆李立大使的主导下，启动了驻摩洛哥使馆的海外党建云平台建设。',
					id: 3
				}, {
					url: '/static/partyBuilding/(30).jpg',
					title: '中国物流股份有限公司党建云',
					content: '据介绍，该区推出的党群e家信息化平台及“365”管理服务模式，通过搭建可视化党建管理平台、党建手机app平台、党建微信公众号平台、党建门户网站平台、党建新视线电视平台、党建大数据分析应用平台，各平台互为补充，推动党建工作的全域覆盖、线上线下相互融合促进。同时，通过构建“区—镇(街道)—村(社区)”三级基层党建工作体系和管理网络，让党建信息化有人来抓、有人来管、有人来干。',
					id: 4
				}]
			}
		},
		methods: {
			clickItem(e) {
				this.current = e.currentIndex
			}
		}
	}
</script>

<style>

</style>