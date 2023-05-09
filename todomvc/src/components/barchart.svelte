<script>
	import * as d3 from "d3";

	let width = 800;
	let height = 300;

	let margin = { top: 10, right: 10, bottom: 20, left: 400 };

	export let data = [];

	$: xScale = d3
		.scaleLinear()
		.domain([d3.min(data, (d) => d.value) > 0 ? 0 : d3.min(data, (d) => d.value), d3.max(data, (d) => d.value)])
		.range([margin.left, width - margin.right]);

	$: yScale = d3
		.scaleBand()
		.domain(data.map((d) => d.type))
		.range([margin.top, height - margin.bottom]);

	let xAxis;
	let yAxis;

	$: {
		d3.select(xAxis).call(d3.axisBottom(xScale));
		d3.select(yAxis).call(d3.axisLeft(yScale));
	}
</script>

<svg {width} {height}>
	{#each data as d, i}
		<rect
			class="bar"
			x={d.value > 0 ? xScale(0) : xScale(d.value)}
			y={yScale(d.type)}
			width={d.value > 0 ? xScale(d.value) - xScale(0) : xScale(0) - xScale(d.value)}
			height={yScale.bandwidth()}
			fill={d.highlight ? "red" : "blue"}
		/>
	{/each}

	<!-- <g transform="translate(0, {height - margin.bottom})"
		 bind:this={xAxis} /> -->

	<g transform="translate({margin.left}, 0)" bind:this={yAxis} />
</svg>

<style>
	.bar {
		stroke: white;
	}
</style>
