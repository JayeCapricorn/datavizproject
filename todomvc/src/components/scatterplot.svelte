<script>
	import * as d3 from 'd3';
	import {onMount} from 'svelte';
	
	let width = 500;
	let height = 400;
	
	let margin = {top: 25, right: 10, bottom: 75, left: 20};
	
	let data = [];
	onMount(async function() {
		data = await d3.csv('https://vega.github.io/vega-datasets/data/gapminder-health-income.csv', (d) => ({
			...d,
			income: +d.income,
			health: +d.health,
			population: +d.population
		}));
		console.log(data);
	});
	
	$: xScale = d3.scaleLog()
		.domain([d3.min(data, d => d.income), d3.max(data, d => d.income)])
		.range([margin.left, width - margin.right]);
	
	$: yScale = d3.scaleLinear()
			.domain([0, d3.max(data, d => d.health)])
			.range([height - margin.bottom, margin.top])
	
	$: sizeScale = d3.scaleSqrt()
			.domain(d3.extent(data, d => d.population))
			.range([5, 50])

	$: colorScale = d3.scaleOrdinal(d3.schemeTableau10)
			.domain(data.map(d => d.region));
	
	let xAxis;
	let yAxis;
	
	$: {
		d3.select(yAxis).call(d3.axisLeft(yScale));
		
		d3.select(xAxis)
				.call(d3.axisBottom(xScale))
				.selectAll('.tick > text')
				.attr('y', 0)
				.attr('dy', '0.35em')
				.attr('dx', '-1em')
				.attr('text-anchor', 'end')
				.attr('transform', 'rotate(-90)');
	}
</script>

<svg {width} {height}>
	{#each data as d, i}
		<circle
					cx={xScale(d.income)}
					cy={yScale(d.health)}
					r={sizeScale(d.population)}
					height={yScale(0) - yScale(d.health)}
					fill={colorScale(d.region)} />
	{/each}
	
	<g transform="translate(0, {height - margin.bottom})"
		 bind:this={xAxis} />
	
	<g transform="translate({margin.left}, 0)"
		 bind:this={yAxis} />
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