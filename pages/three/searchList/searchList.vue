<template>
	<view>
		<view v-for="(item,index) in CC" :key="index">
			<navigator :url="`../Deatil/Deatil?id=${JSON.stringify(item)}`">
				<uni-list>
					<uni-list-item title="" note="">
						<template v-slot:body>
							<image style="margin-right: 5%;" :src="item.url" mode=""></image>
							<view style="width: 60%;">
								<view class="" style="font-size: 16px;font-weight: 700;">{{item.title}}</view>
								<rich-text class="text_All" style="font-size: 15px;"
									:nodes="item.content.slice(0,50)+'...'"></rich-text>
							</view>
						</template>
					</uni-list-item>
				</uni-list>
			</navigator>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '',
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
				CC: []
			}
		},
		onLoad(e) {
			this.title = e.title

			for (let i = 0; i < this.list.length; i++) {
				if (this.list[i].title.indexOf(this.title) > -1) {
					this.CC.push(this.list[i])
				}
			}
		},
		methods: {

		}
	}
</script>

<style>

</style>