<script>
	import * as d3 from "d3";
	$: innerWidth = 1920;
    $: chartWidth = innerWidth * 0.65;
    $: chartHeight = innerWidth * 0.25;
	$: centerX = chartWidth / 2 + 40;
    $: centerY = chartHeight / 2;

	// let width = 1200;
	// let height = 300;

	const paddings = {
        top: 30,
        left: 750,
        right: 0,
        bottom: 30,
    };

	// let margin = { top: 10, right: 0, bottom: 20, left: 800 };

	export let data = [];
	export let title = "";

	$: xScale = d3
		.scaleLinear()
		.domain([
			d3.min(data, (d) => d.value) > 0 ? 0 : d3.min(data, (d) => d.value),
			d3.max(data, (d) => d.value),
		])
		.range([paddings.left, chartWidth  - paddings.right]);

	$: yScale = d3
		.scaleBand()
		.domain(data.map((d) => d.type))
		.range([paddings.top, chartHeight - paddings.bottom])
		.padding(0.5);

	let xAxis;
	let yAxis;

	$: {
		d3.select(xAxis).call(d3.axisBottom(xScale));
		d3.select(yAxis)
			.call(d3.axisLeft(yScale).tickSize(0).tickPadding(10))
			.selectAll(".domain, .tick line")
			.style("stroke", "none");
		d3.select(yAxis).selectAll(".tick > text").style("font-size", "15px");
	}

	// const centerX = chartWidth / 2;
	// const centerY = height / 2;
	let has_negative = false;
	data.forEach((d) => {
		if (d.value < 0) {
			has_negative = true;
		}
	});
	let right_shift = has_negative ? 40 : 0;
</script>
<svelte:window bind:innerWidth/>
<h4 class="title">{title}</h4>
<svg width={chartWidth} height={chartHeight} >
	{#each data as d, i}
		<rect
			class="bar"
			x={d.value > 0
				? centerX -
				  (chartWidth - paddings.left - paddings.right) / 2 +
				  xScale(0) -
				  paddings.left +
				  right_shift
				: centerX -
				  (chartWidth - paddings.left - paddings.right) / 2 +
				  xScale(d.value) -
				  paddings.left +
				  right_shift}
			y={centerY -
				(chartHeight - paddings.top - paddings.bottom) / 2 +
				yScale(d.type) -
				paddings.top + 5}
			width={d.value > 0
				? xScale(d.value) - xScale(0)
				: xScale(0) - xScale(d.value)}
			height={yScale.bandwidth()}
			fill={d.highlight ? "#CA4825" : "#176695"}
		/>
		<text
			x={d.value > 0
				? centerX -
				  (chartWidth - paddings.left - paddings.right) / 2 -
				  paddings.left +
				  xScale(d.value) +
				  right_shift +
				  10
				: centerX -
				  (chartWidth - paddings.left - paddings.right) / 2 +
				  xScale(d.value) -
				  paddings.left -
				  (d.value + "").length * 10 +
				  right_shift +
				  10}
			y={centerY -
				(chartHeight - paddings.top - paddings.bottom) / 2 +
				yScale(d.type) -
				paddings.top +
				yScale.bandwidth() / 2 +
				10}
			fill={d.highlight ? "#CA4825" : "#176695"}>{d.value}</text
		>
	{/each}
	<!-- <g transform={`translate(0, ${centerY + (height - margin.top - margin.bottom) / 2})`}
		 bind:this={xAxis} /> -->
	<g
		transform={`translate(${
			centerX - (chartWidth - paddings.left - paddings.right) / 2
		}, 5)`}
		bind:this={yAxis}
	/>
</svg>

<style>
	.bar {
		/* stroke: white; */
		opacity: 0.8;
	}

	.title {
		font: 20px 'Open Sans', sans-serif;
		font-weight: 900;
		margin-bottom: -20px;
		margin-top: -0px;
	}
</style>
