<template>
	<view>
		<uni-section title="课程列表" sub-title="" type="line">
			<uni-segmented-control :current="current" :values="text" @clickItem="clickItem"></uni-segmented-control>
			<view class="content">
				<view v-show="current === 0">
					<uni-collapse v-for="(item,index) in list.slice(0,3)" :key="index">
						<uni-collapse-item :title="item.title">
							<view class="content">
								<image :src="item.url" mode=""></image>
								<view>{{item.content}}</view>
								<uni-section title="视频" sub-title="" type="line">
									<video src="../../../static/mv/one.mp4" style="width: 100%;" controls></video>
								</uni-section>
								<uni-section title="音频" sub-title="" type="line">
									<audio src="../../../static/mv/two.mp3" style="width: 100%;"  controls></audio>
								</uni-section>
							</view>
						</uni-collapse-item>
					</uni-collapse>
				</view>
				<view v-show="current === 1">
					<uni-collapse v-for="(item,index) in list.slice(3,6)" :key="index">
						<uni-collapse-item :title="item.title">
							<view class="content">
								<image :src="item.url" mode=""></image>
								<view>{{item.content}}</view>
								<uni-section title="视频" sub-title="" type="line">
									<video src="../../../static/mv/one.mp4" style="width: 100%;" controls></video>
								</uni-section>
								<uni-section title="音频" sub-title="" type="line">
									<audio src="../../../static/mv/two.mp3" style="width: 100%;"  controls></audio>
								</uni-section>
							</view>
						</uni-collapse-item>
					</uni-collapse>
				</view>
				<view v-show="current === 2">
					<uni-collapse v-for="(item,index) in list.slice(6,9)" :key="index">
						<uni-collapse-item :title="item.title">
							<view class="content">
								<image :src="item.url" mode=""></image>
								<view>{{item.content}}</view>
								<uni-section title="视频" sub-title="" type="line">
									<video src="../../../static/mv/one.mp4" style="width: 100%;" controls></video>
								</uni-section>
								<uni-section title="音频" sub-title="" type="line">
									<audio src="../../../static/mv/two.mp3" style="width: 100%;"  controls></audio>
								</uni-section>
							</view>
						</uni-collapse-item>
					</uni-collapse>
				</view>
			</view>
			
			<uni-section title="课程评论" sub-title="" type="line" >
				<uni-forms ref="form" style="margin: 50rpx;">
					<uni-forms-item label="标题" name="">
						<uni-easyinput v-model="title" placeholder="" />
					</uni-forms-item>
					<uni-forms-item label="内容" name="">
						<textarea v-model="content" maxlength="150"
							style="width: 100%; border: 1px solid black;"></textarea>
						字数{{content.length}}/150
					</uni-forms-item>
					<button type="primary" style="margin: 50rpx;" @click="commit">评论</button>
				</uni-forms>
			</uni-section>
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				current: 0,
				title: "",
				content: "",
				text: ['C语言', 'C#', 'C++'],
				list: [{
						url: '/static/partyBuilding/(17).jpg',
						title: '中国建筑标准设计研究院党建云',
						content: '为进一步加强党务共建与政企交流，深入创新党建工作,2020年12月21日，温州机场集团机关直属第一党支部、第二党支部与国航股份有限公司温州分公司机关党支部共同参加了由浙江省空港贵宾服务有限公司第四党支部牵头组织的赴正泰集团开展党务共建暨主题党日活动。',
						id: 0
					}, {
						url: '/static/partyBuilding/(18).jpg',
						title: '中国物流股份有限公司党建云',
						content: '为进一步加强党务共建与政企交流，深入创新党建工作,2020年12月21日，温州机场集团机关直属第一党支部、第二党支部与国航股份有限公司温州分公司机关党支部共同参加了由浙江省空港贵宾服务有限公司第四党支部牵头组织的赴正泰集团开展党务共建暨主题党日活动。',
						id: 2
					}, {
						url: '/static/partyBuilding/(19).jpg',
						title: '中国建筑标准设计研究院党建云',
						content: '　为贯彻落实习近平总书记加强国有企业境外单位党的建设要求，为30余家驻摩洛哥中资企业、机构建立一个党建平台，将党建工作纳入统一管理，成为加强海外党建工作的有力抓手，2018年5月，在中国驻摩洛哥使馆李立大使的主导下，启动了驻摩洛哥使馆的海外党建云平台建设。',
						id: 3
					}, {
						url: '/static/partyBuilding/(20).jpg',
						title: '中国物流股份有限公司党建云',
						content: '据介绍，该区推出的党群e家信息化平台及“365”管理服务模式，通过搭建可视化党建管理平台、党建手机app平台、党建微信公众号平台、党建门户网站平台、党建新视线电视平台、党建大数据分析应用平台，各平台互为补充，推动党建工作的全域覆盖、线上线下相互融合促进。同时，通过构建“区—镇(街道)—村(社区)”三级基层党建工作体系和管理网络，让党建信息化有人来抓、有人来管、有人来干。',
						id: 4
					}, {
						url: '/static/partyBuilding/(21).jpg',
						title: '中国物流股份有限公司党建云',
						content: '在“全国石油物探企业党建思想政治工作企业文化研究会2019年年会”期间，来自中国石油、中国石化、中国海油等29个会员单位的90余名领导和代表参观中油瑞飞“智慧党建活动室”，现场观摩了“守初心、担使命、亮承诺”的主题党日活动，体验VR产品。现场领导和代表都对党建VR一体机、智能会议纪要系统等智能党建产品给予了高度的评价。',
						id: 5
					},
					{
						url: '/static/partyBuilding/(22).jpg',
						title: '中国物流股份有限公司党建云',
						content: '在“全国石油物探企业党建思想政治工作企业文化研究会2019年年会”期间，来自中国石油、中国石化、中国海油等29个会员单位的90余名领导和代表参观中油瑞飞“智慧党建活动室”，现场观摩了“守初心、担使命、亮承诺”的主题党日活动，体验VR产品。现场领导和代表都对党建VR一体机、智能会议纪要系统等智能党建产品给予了高度的评价。',
						id: 6
					},
					{
						url: '/static/partyBuilding/(24).jpg',
						title: '中国建筑标准设计研究院党建云',
						content: '为进一步加强党务共建与政企交流，深入创新党建工作,2020年12月21日，温州机场集团机关直属第一党支部、第二党支部与国航股份有限公司温州分公司机关党支部共同参加了由浙江省空港贵宾服务有限公司第四党支部牵头组织的赴正泰集团开展党务共建暨主题党日活动。',
						id: 7
					}, {
						url: '/static/partyBuilding/(25).jpg',
						title: '中国物流股份有限公司党建云',
						content: '为进一步加强党务共建与政企交流，深入创新党建工作,2020年12月21日，温州机场集团机关直属第一党支部、第二党支部与国航股份有限公司温州分公司机关党支部共同参加了由浙江省空港贵宾服务有限公司第四党支部牵头组织的赴正泰集团开展党务共建暨主题党日活动。',
						id: 9
					}, {
						url: '/static/partyBuilding/(26).jpg',
						title: '中国建筑标准设计研究院党建云',
						content: '　为贯彻落实习近平总书记加强国有企业境外单位党的建设要求，为30余家驻摩洛哥中资企业、机构建立一个党建平台，将党建工作纳入统一管理，成为加强海外党建工作的有力抓手，2018年5月，在中国驻摩洛哥使馆李立大使的主导下，启动了驻摩洛哥使馆的海外党建云平台建设。',
						id: 10
					},
				]
			}
		},
		methods: {
			clickItem(e) {
				this.current = e.currentIndex
			},
			commit() {
				uni.showToast({
					title: '评论成功'
				});
				this.title = ""
				this.content = ""
			}
		}
	}
</script>

<style>

</style>