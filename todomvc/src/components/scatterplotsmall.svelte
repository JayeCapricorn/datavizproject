<script>
	import * as d3 from "d3";

	 // set general use variables
	$: innerWidth = 1920;
    $: chartWidth = innerWidth * 0.40;
    $: chartHeight = innerWidth * 0.13;

	// let width = 400;
	// let height = 300;

	const paddings = {
        top: 30,
        left: 100,
        right: 80,
        bottom: 30,
    };

	// let margin = { top: 25, right: 10, bottom: 75, left: 50 };

	export let data = [];
	export let ols = {}; // {"x0": x0, "y0": y0, "x1": x1, "y1": y1}
	export let title = "";

	$: xScale = d3
		.scaleLinear()
		.domain([d3.min(data, (d) => d.x), d3.max(data, (d) => d.x)])
		.range([paddings.left, chartWidth - paddings.right]);

	$: yScale = d3
		.scaleLinear()
		.domain([0, d3.max(data, (d) => d.y)])
		.range([chartHeight - paddings.bottom, paddings.top]);

	$: sizeScale = d3
		.scaleSqrt()
		.domain(d3.extent(data, (d) => d.population))
		.range([5, 50]);

	const countryColors = {
		Honduras: "#c15133",
		'El Salvador': "#F39600",
		Guatemala: '#107486',
	};

	$: colorScale = (country) => countryColors[country];

	let xAxis;
	let yAxis;

	$: {
		d3.select(yAxis).call(d3.axisLeft(yScale));

		d3.select(xAxis)
			.call(d3.axisBottom(xScale))
			.selectAll(".tick > text")
			.attr("y", 0)
			.attr("dy", "0.35em")
			.attr("dx", "-1em")
			.attr("text-anchor", "end")
			.attr("transform", "rotate(-90)");
	}

	let legendItemWidth = 90;
	let legend = {
		// x: chartWidth / 2 - (3 * legendItemWidth) / 2 + 80,
		// y: chartHeight - paddings.bottom + 40,
	};
</script>

<svelte:window bind:innerWidth/>


<h4 class="title">{title}</h4>

<svg
	width={chartWidth}
	height={chartHeight + 50}
>
	{#each data as d, i}
		<circle
			cx={xScale(d.x)}
			cy={yScale(d.y)}
			r="7"
			height={yScale(0) - yScale(d.y)}
			fill={colorScale(d.country)}
		/>
	{/each}

	{#if ols.x0}
		<line
			x1={xScale(ols.x0)}
			y1={yScale(ols.y0)}
			x2={xScale(ols.x1)}
			y2={yScale(ols.y1)}
			stroke="black"
			stroke-width="2"
		/>
	{/if}

	<g transform="translate(0, {chartHeight - paddings.bottom})" bind:this={xAxis} />

	<g transform="translate({paddings.left}, 0)" bind:this={yAxis} />

	<g transform="translate({chartWidth / 2 - (3 * legendItemWidth) / 2 - 50}, {chartHeight - paddings.bottom + 50})" class="legend">
		{#each Object.entries(countryColors) as [country, color], i}
			<!-- if there is no data from this country, skip -->
			{#if data.filter((d) => d.country === country).length > 0}
				<circle cx={i * legendItemWidth+72} cy="5" r="5" fill={color} />
				<text x={i * legendItemWidth + 85} y="10" >{country}</text>
			{/if}
		{/each}
	</g>
</svg>


<style>
	@import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@300&display=swap");
	/* svg {
		border: 2px dashed goldenrod;
	} */

	circle {
		fill-opacity: 0.55;
		/* stroke: white; */
	}

	.legend{
		font: 12px 'Open Sans', sans-serif;
	}

	.title {
		font: 20px 'Open Sans', sans-serif;
		font-weight: 900;
		margin-bottom: -10px;
	}

</style>
