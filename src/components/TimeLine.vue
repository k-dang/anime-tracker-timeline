<template>
	<div id="visualization" ref="visualization"></div>
</template>

<script>
import vis from 'vis'
let testData = require('./../data/mock.json')

export default {
	data() {
		return {
			title: "Vis TimeLine",
			items: null,
			groups: [],
			options: {}
		}
	},
	created() {
		let previousDate = new Date();
		previousDate.setDate(previousDate.getDate() - 1);
		let futureDate = new Date();
		futureDate.setDate(futureDate.getDate() + 7);

		this.options = {
			min: previousDate,
			max: futureDate,
			zoomMax: 604800000,
			zoomMin: 604800000,
			verticalScroll: true,
			maxHeight: window.innerHeight,
		}

		// eslint-disable-next-line
		console.log(testData);
		this.items = new vis.DataSet([]);
		
		testData.forEach((series, index) => {
			let label_content = series.title ? series.title : series.title_alt
			this.groups.push({
				id: index + 1,
				content: `
					<div>
						<img src="${series.image_url}">
						<h3>${label_content}</h3>
					</div>
				`
			})

			series.episodes.forEach((date, ep) => {
				if (new Date(date) > new Date() && new Date(date) < futureDate) {
					this.items.add({
						title: `${new Date(date)}`,
						content: `<h3>Episode ${ep + 1}</h3>`,
						start: new Date(date),
						group: index + 1
					});
				}
			})
		})
	},
	mounted(){
		new vis.Timeline(this.$refs.visualization, this.items, this.groups, this.options);
	}

}
</script>

<style>
	.vis-timeline {
		background: #19191d;
		border: none;
	}

	.vis-labelset .vis-label {
		color: white;
	}

	.vis-time-axis .vis-text {
		color: white;
	}

	.vis-item {
		color: white;
		border-color: white;
		background-color: #2c3e50;
	}

	.vis-item.vis-selected {
		border-color: white;
		background-color: #262626;
	}
</style>
