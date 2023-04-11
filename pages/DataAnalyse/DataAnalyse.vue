<template>
	<view>
		<uni-section title="双柱图" sub-title="" type="line">
			<qiun-data-charts type="column" :chartData="chartData1" :ontouch="true" />
		</uni-section>
		<uni-section title="折现图" sub-title="" type="line">
			<qiun-data-charts type="line" :chartData="chartData2" />
		</uni-section>
		<uni-section title="饼图" sub-title="" type="line">
			<qiun-data-charts type="pie" :chartData="chartData3" />
		</uni-section>
		<uni-section title="混合图" sub-title="" type="line">
			<qiun-data-charts type="mix" :chartData="chartData4" />
		</uni-section>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				chartData1: {},
				chartData2: {},
				chartData3: {},
				chartData4: {},
			}
		},
		onLoad() {
			this.getServerData1();
			this.getServerData2();
			this.getServerData3();
			this.getServerData4();
		},
		methods: {
			getServerData1() {
				//模拟从服务器获取数据时的延时
				setTimeout(() => {
					//模拟服务器返回数据，如果数据格式和标准格式不同，需自行按下面的格式拼接
					let res = {
						categories: ["2018", "2019", "2020", "2021", "2022", "2023"],
						series: [{
								name: "目标值",
								data: [35, 36, 31, 33, 13, 34]
							},
							{
								name: "完成量",
								data: [18, 27, 21, 24, 6, 28]
							}
						]
					};
					this.chartData1 = JSON.parse(JSON.stringify(res));
				}, 500);
			},
			getServerData2() {
				//模拟从服务器获取数据时的延时
				setTimeout(() => {
					//模拟服务器返回数据，如果数据格式和标准格式不同，需自行按下面的格式拼接
					let res = {
						categories: ["2018", "2019", "2020", "2021", "2022", "2023"],
						series: [{
								name: "成交量A",
								data: [35, 8, 25, 37, 4, 20]
							},
							{
								name: "成交量B",
								data: [70, 40, 65, 100, 44, 68]
							},
							{
								name: "成交量C",
								data: [100, 80, 95, 150, 112, 132]
							}
						]
					};
					this.chartData2 = JSON.parse(JSON.stringify(res));
				}, 500);
			},
			getServerData3() {
				//模拟从服务器获取数据时的延时
				setTimeout(() => {
					//模拟服务器返回数据，如果数据格式和标准格式不同，需自行按下面的格式拼接
					let res = {
						series: [{
							data: [{
								"name": "一班",
								"value": 50
							}, {
								"name": "二班",
								"value": 30
							}, {
								"name": "三班",
								"value": 20
							}, {
								"name": "四班",
								"value": 18
							}, {
								"name": "五班",
								"value": 8
							}]
						}]
					};
					this.chartData3 = JSON.parse(JSON.stringify(res));
				}, 500);
			},
			getServerData4() {
				//模拟从服务器获取数据时的延时
				setTimeout(() => {
					//模拟服务器返回数据，如果数据格式和标准格式不同，需自行按下面的格式拼接
					let res = {
						categories: ["2018", "2019", "2020", "2021", "2022", "2023"],
						series: [{
								name: "曲面",
								type: "area",
								style: "curve",
								data: [70, 50, 85, 130, 64, 88]
							},
							{
								name: "柱1",
								index: 1,
								type: "column",
								data: [40, {
									"value": 30,
									"color": "#f04864"
								}, 55, 110, 24, 58]
							},
							{
								name: "柱2",
								index: 1,
								type: "column",
								data: [50, 20, 75, 60, 34, 38]
							},
							{
								name: "曲线",
								type: "line",
								style: "curve",
								color: "#1890ff",
								disableLegend: true,
								data: [70, 50, 85, 130, 64, 88]
							},
							{
								name: "折线",
								type: "line",
								color: "#2fc25b",
								data: [120, 140, 105, 170, 95, 160]
							},
							{
								name: "点",
								index: 2,
								type: "point",
								color: "#f04864",
								data: [100, 80, 125, 150, 112, 132]
							}
						]
					};
					this.chartData4 = JSON.parse(JSON.stringify(res));
				}, 500);
			},
		},

	};
</script>

<style>

</style>