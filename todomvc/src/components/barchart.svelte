<script>
	// import { fly, draw } from "svelte/transition";
	// import { cubicOut, cubicInOut } from "svelte/easing";
	import * as d3 from 'd3';
	import {onMount} from 'svelte';
	
	let width = 500;
	let height = 400;
	
	let margin = {top: 10, right: 10, bottom: 20, left: 20};
	
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
	
	$: xScale = d3.scaleBand()
		.domain(data.map(d => d.country))
		.range([margin.left, width - margin.right]);
	
	$: yScale = d3.scaleLinear()
			.domain([0, d3.max(data, d => d.health)])
			.range([height - margin.bottom, margin.top])

	$: colorScale = d3.scaleOrdinal(d3.schemeTableau10)
		.domain(data.map(d => d.region));
	
	let xAxis;
	let yAxis;
	
	$: {
		d3.select(xAxis).call(d3.axisBottom(xScale));
		d3.select(yAxis).call(d3.axisLeft(yScale));
	}
</script>

<svg {width} {height}>

	{#each data as d, i}
		<rect class="bar"
					x={xScale(d.country)}
					y={yScale(d.health)}
					width={xScale.bandwidth()}
					height={yScale(0) - yScale(d.health)}
					fill={colorScale(d.region)} />
	{/each}
	
	<!-- <g transform="translate(0, {height - margin.bottom})"
		 bind:this={xAxis} /> -->
	
	<g transform="translate({margin.left}, 0)"
		 bind:this={yAxis} />
</svg>

<style>
	/* svg {
		border: 2px dashed goldenrod;	
	} */
	
	.bar {
		stroke: white;
	}
</style>