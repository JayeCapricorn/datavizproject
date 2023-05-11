<script>
	import * as d3 from "d3";

	let width = 1200;
	let height = 300;

	let margin = { top: 10, right: 0, bottom: 20, left: 800 };

	export let data = [];

	$: xScale = d3
		.scaleLinear()
		.domain([
			d3.min(data, (d) => d.value) > 0 ? 0 : d3.min(data, (d) => d.value),
			d3.max(data, (d) => d.value),
		])
		.range([margin.left, width - margin.right]);

	$: yScale = d3
		.scaleBand()
		.domain(data.map((d) => d.type))
		.range([margin.top, height - margin.bottom])
		.padding(0.5);

	let xAxis;
	let yAxis;

	$: {
		d3.select(xAxis).call(d3.axisBottom(xScale));
		d3.select(yAxis)
			.call(d3.axisLeft(yScale).tickSize(0).tickPadding(10))
			.selectAll(".domain, .tick line")
			.style("stroke", "none");
	}

	const centerX = width / 2;
	const centerY = height / 2;
	let has_negative = false;
	data.forEach((d) => {
		if (d.value < 0) {
			has_negative = true;
		}
	});
	let right_shift = has_negative ? 40 : 0;
</script>

<svg {width} {height} viewBox={`0 0 ${width} ${height}`}>
	{#each data as d, i}
		<rect
			class="bar"
			x={d.value > 0
				? centerX -
				  (width - margin.left - margin.right) / 2 +
				  xScale(0) -
				  margin.left +
				  right_shift
				: centerX -
				  (width - margin.left - margin.right) / 2 +
				  xScale(d.value) -
				  margin.left +
				  right_shift}
			y={centerY -
				(height - margin.top - margin.bottom) / 2 +
				yScale(d.type) -
				margin.top}
			width={d.value > 0
				? xScale(d.value) - xScale(0)
				: xScale(0) - xScale(d.value)}
			height={yScale.bandwidth()}
			fill={d.highlight ? "red" : "blue"}
		/>
		<text
			x={d.value > 0
				? centerX -
				  (width - margin.left - margin.right) / 2 -
				  margin.left +
				  xScale(d.value) +
				  right_shift +
				  10
				: centerX -
				  (width - margin.left - margin.right) / 2 +
				  xScale(d.value) -
				  margin.left -
				  (d.value + "").length * 10 +
				  right_shift +
				  10}
			y={centerY -
				(height - margin.top - margin.bottom) / 2 +
				yScale(d.type) -
				margin.top +
				yScale.bandwidth() / 2 +
				5}
			fill={d.highlight ? "red" : "blue"}>{d.value}</text
		>
	{/each}
	<!-- <g transform={`translate(0, ${centerY + (height - margin.top - margin.bottom) / 2})`}
		 bind:this={xAxis} /> -->
	<g
		transform={`translate(${
			centerX - (width - margin.left - margin.right) / 2
		}, 5)`}
		bind:this={yAxis}
	/>
</svg>

<style>
	.bar {
		stroke: white;
	}
</style>
