<template>
	<view>
		<uni-search-bar @confirm="confirm" @input="" placeholder="请输入搜索关键字" />
		<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
			<swiper-item v-for="(item,index) in sp" :key="index">
				<navigator :url="`newDetail/newDetail?id=${item.id}`" style="height: 100%;">
					<image :src="item.url" style="width: 100%; height: 100%;"></image>
				</navigator>
			</swiper-item>
		</swiper>

		<uni-section title="党建服务入口" sub-title="" type="line">
			<uni-grid :column="5" :showBorder="false">
				<uni-grid-item>
					<view class="imgs">
						<navigator url="Partybuildingtrends/Partybuildingtrends">
							<image src="../../static/partyBuilding/(6).jpg"
								style="width: 80rpx; height: 80rpx; border-radius: 50%;" mode="">
							</image>
							<view>党建动态</view>
						</navigator>
					</view>
				</uni-grid-item>
				<uni-grid-item>
					<view class="imgs">
						<navigator url="Partymemberstudy/Partymemberstudy">
							<image src="../../static/partyBuilding/(7).jpg"
								style="width: 80rpx; height: 80rpx; border-radius: 50%;" mode="">
							</image>
							<view>党员学习</view>
						</navigator>
					</view>
				</uni-grid-item>
				<uni-grid-item>
					<view class="imgs">
						<navigator url="Organizeactivities/Organizeactivities">
							<image src="../../static/partyBuilding/(8).jpg"
								style="width: 80rpx; height: 80rpx; border-radius: 50%;" mode="">
							</image>
							<view>组织活动</view>
						</navigator>
					</view>
				</uni-grid-item>
				<uni-grid-item>
					<view class="imgs">
						<navigator url="Offeradviceandsuggestions/Offeradviceandsuggestions">
							<image src="../../static/partyBuilding/(9).jpg"
								style="width: 80rpx; height: 80rpx; border-radius: 50%;" mode="">
							</image>
							<view>建言献策</view>
						</navigator>
					</view>
				</uni-grid-item>
				<uni-grid-item>
					<view class="imgs">
						<navigator url="Randomclap/Randomclap">
							<image src="../../static/partyBuilding/(10).jpg"
								style="width: 80rpx; height: 80rpx; border-radius: 50%;" mode="">
							</image>
							<view>随手拍</view>
						</navigator>
					</view>
				</uni-grid-item>
			</uni-grid>

		</uni-section>
		<uni-section title="热门党建新闻" sub-title="" type="line">
			<uni-grid :column="2" :showBorder="false">
				<uni-grid-item v-for="(item,index) in hot" :key="index">
					<navigator :url="`Deatil/Deatil?id=${JSON.stringify(item)}`" style="height: 100%;">
						<view class="imgs">
							<image :src="item.url" style="width: 320rpx; height: 320rpx; border-radius: 20rpx;" mode="">
							</image>
							<view>{{item.title?item.title.slice(0,13)+'...':''}}</view>
						</view>
					</navigator>
				</uni-grid-item>
			</uni-grid>
		</uni-section>

		<uni-section title="新闻列表" sub-title="" type="line">
			<view v-for="(item,index) in list" :key="index">
				<uni-card>
					<navigator :url="`Deatil/Deatil?id=${JSON.stringify(item)}`" style="height: 100%;">
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
				list: [{
					url: '/static/partyBuilding/(13).jpg',
					title: '中国建筑标准设计研究院党建云',
					content: '　为贯彻落实习近平总书记加强国有企业境外单位党的建设要求，为30余家驻摩洛哥中资企业、机构建立一个党建平台，将党建工作纳入统一管理，成为加强海外党建工作的有力抓手，2018年5月，在中国驻摩洛哥使馆李立大使的主导下，启动了驻摩洛哥使馆的海外党建云平台建设。',
					id: 0
				}, {
					url: '/static/partyBuilding/(14).jpg',
					title: '中国物流股份有限公司党建云',
					content: '人民日报评论：坚持以维护党中央权威为统领加强党对对外工作的集中统一领导。办好中国的事情，关键在党。我们要坚持外交大权在党中央，加强对外工作的集中统一领导和统筹协调，形成党总揽全局、协调各方的对外工作大协同局面。',
					id: 1
				}, {
					url: '/static/partyBuilding/(15).jpg',
					title: '中国建筑标准设计研究院党建云',
					content: '　为贯彻落实习近平总书记加强国有企业境外单位党的建设要求，为30余家驻摩洛哥中资企业、机构建立一个党建平台，将党建工作纳入统一管理，成为加强海外党建工作的有力抓手，2018年5月，在中国驻摩洛哥使馆李立大使的主导下，启动了驻摩洛哥使馆的海外党建云平台建设。',
					id: 2
				}, {
					url: '/static/partyBuilding/(16).jpg',
					title: '中国物流股份有限公司党建云',
					content: '人民日报评论：坚持以维护党中央权威为统领加强党对对外工作的集中统一领导。办好中国的事情，关键在党。我们要坚持外交大权在党中央，加强对外工作的集中统一领导和统筹协调，形成党总揽全局、协调各方的对外工作大协同局面。',
					id: 3
				}],
				icon: [],
				hot: [{
					url: '/static/partyBuilding/(11).jpg',
					title: '中国建筑标准设计研究院党建云',
					content: '　为贯彻落实习近平总书记加强国有企业境外单位党的建设要求，为30余家驻摩洛哥中资企业、机构建立一个党建平台，将党建工作纳入统一管理，成为加强海外党建工作的有力抓手，2018年5月，在中国驻摩洛哥使馆李立大使的主导下，启动了驻摩洛哥使馆的海外党建云平台建设。',
					id: 0
				}, {
					url: '/static/partyBuilding/(12).jpg',
					title: '中国物流股份有限公司党建云',
					content: '人民日报评论：坚持以维护党中央权威为统领加强党对对外工作的集中统一领导。办好中国的事情，关键在党。我们要坚持外交大权在党中央，加强对外工作的集中统一领导和统筹协调，形成党总揽全局、协调各方的对外工作大协同局面。',
					id: 1
				}],
				sp: [{
					url: '/static/partyBuilding/(1).jpg',
					title: '高效督促党员自觉参与学习',
					content: '微加智慧党建的微党课，根据组织需求上传符合学校的学习资料、文件，不仅可以上传图文资料还能上传视频资料。使用前:组织内的学习培训任务很难有量化的检测，谁学谁没学，学了多少都比较模糊。使用后:平台自动记录每名党员的学习时长，学习课程明细，并且以积分的形式激励党员积极参加组织内的学习培训，极大地激发了党员的自主学习意识，并且学习完后平台提供在线考试进行学习效果评测，从学习，到强化，做到内化于心，外化于行。',
					id: 0
				}, {
					url: '/static/partyBuilding/(2).jpg',
					title: '高效传达组织声音给基层',
					content: '政策法规，党章党规，会务通知、最新党内动态、中央会议精神等文件、资讯可以一键发布给组织内的成员。使用前:通知、消息发出后，党内成员有没有收到，有没有阅读都是无从了解。使用后:消息直接传达给组织内党员，谁读了谁没读，系统后台自动记录，对未读人员可再次发起阅读提醒，对已读人员给予积分激励，提高党员主动接收组织声音的积极性。',
					id: 1
				}, {
					url: '/static/partyBuilding/(3).jpg',
					title: '思想汇报不再只是面对面',
					content: '党员通过移动党建平台，随时随地向组织汇报心得体会，方便组织了解党员思想状况。使用前:组织内直接找党员面对面沟通交流，不仅耗时耗力，而且效率也不高。使用后:党员学习心得体会、观影心得体会等学习培训感想实时通过手机向组织汇报，让组织掌握每名党员的所思所想，一旦发现问题，可及时面对面与党员沟通并发现问题、解决问题。',
					id: 2
				}, {
					url: '/static/partyBuilding/(4).jpg',
					title: '塔里木油田：智慧党建激发活力',
					content: '二是支部生活日益“规范化”。为避免党建线上生活“落而不实、抓而不紧、行而不严”，油田推广应用小组将线上指导、线下督导、制度规范、宣传导向、活动激励、阶段评价有机结合，最大限度地调动党员干部参与度，激发创先争优热情。二级党组织落实党建责任制，确定“三会一课”“时间表”、“任务书”，对党费缴纳实行“清单式”督查，并将落实情况纳入党建目标管理考核。宣传的辐射、活动的激励、压力的传导等形成抓党建合力，促进党建平台工作规范有效落实。',
					id: 3
				}, {
					url: '/static/partyBuilding/(5).jpg',
					title: '条块联动，“四化”绘制党务工作新景象',
					content: '一是党员学习实现“随身化”。石油党建APP与党组织的政治优势充分结合，似丰富多样的“自助餐”，每名党员可以根据自己的不同需求摄取“精神食粮”，在这里，党员不仅可以汲取最新党政动态、时事政策、上级精神等党务知识“营养”，还可以吸收党务工作技能提升“能量”，亦能从“电子书屋”中拓展视野、博闻强识，还可通过“在线答题”、“专家问答”随时随地自主“加餐”，党员“碎片化”时间的合理利用，助推了党员教育的“随身化”。',
					id: 4
				}]
			}
		},
		methods: {
			confirm(e) {
				uni.navigateTo({
					url: 'searchList/searchList?title=' + e.value
				})
			}
		}
	}
</script>

<style>

</style>