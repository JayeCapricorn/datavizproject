<script>
	import * as d3 from "d3";

	let width = 400;
	let height = 300;

	let margin = { top: 25, right: 10, bottom: 75, left: 50 };

	export let data = [];
	export let ols = {}; // {"x0": x0, "y0": y0, "x1": x1, "y1": y1}
	export let title = "";

	$: xScale = d3
		.scaleLinear()
		.domain([d3.min(data, (d) => d.x), d3.max(data, (d) => d.x)])
		.range([margin.left, width - margin.right]);

	$: yScale = d3
		.scaleLinear()
		.domain([0, d3.max(data, (d) => d.y)])
		.range([height - margin.bottom, margin.top]);

	$: sizeScale = d3
		.scaleSqrt()
		.domain(d3.extent(data, (d) => d.population))
		.range([5, 50]);

	const countryColors = {
		Honduras: "red",
		"El Salvador": "green",
		Guatemala: "blue",
	};

	$: colorScale = (country) => countryColors[country];

	// $: colorScale = d3
	// 	.scaleOrdinal(d3.schemeTableau10)
	// 	.domain(data.map((d) => d.country));

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

	// function uniqueCountries(data) {
	// 	return Array.from(new Set(data.map((d) => d.country))).map((country) => ({
	// 		country,
	// 		color: colorScale(country),
	// 	}));
	// }

	let legendItemWidth = 100;
	let legend = {
		x: width / 2 - (3 * legendItemWidth) / 2 + 40,
		y: height - margin.bottom + 40,
	};
</script>

<h4>{title}</h4>

<svg {width} {height}>
	{#each data as d, i}
		<circle
			cx={xScale(d.x)}
			cy={yScale(d.y)}
			r="5"
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

	<g transform="translate(0, {height - margin.bottom})" bind:this={xAxis} />

	<g transform="translate({margin.left}, 0)" bind:this={yAxis} />

	<g transform="translate({legend.x}, {legend.y})" class="legend">
		{#each Object.entries(countryColors) as [country, color], i}
			<!-- if there is no data from this country, skip -->
			{#if data.filter((d) => d.country === country).length > 0}
				<circle cx={i * legendItemWidth} cy="5" r="5" fill={color} />
				<text x={i * legendItemWidth + 15} y="10" font-size="12">{country}</text>
			{/if}
		{/each}
	</g>
</svg>

<style>
	svg {
		/* border: 2px dashed goldenrod;	 */
	}

	circle {
		fill-opacity: 0.75;
		stroke: white;
	}
</style>
