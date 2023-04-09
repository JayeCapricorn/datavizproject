<script>
	import * as d3 from 'd3';
	import {onMount} from 'svelte';
	export let data;

	var addZeros = d3.format("04d");
	
    let hazards = ["Earthquake", "Flood", "Cyclone", "Eruption"];
	let coloroptions = {"Earthquake": "orange", "Flood" : "blue", "Cyclone": "teal", "Eruption": "gold"};
	let hovered = -1; 
	let recorded_mouse_position = {
		x: 0, y: 0
	};
	
	let width = 1000;
	let height = 400;
	
	let margin = {top: 10, right: 50, bottom: 25, left: 100};
	
	
	$: xScale = d3.scaleLinear()
		.domain([1900, 2022])
		.range([margin.left, width - margin.right]);
// 1539

	$: sizeScale = d3.scaleSqrt()
		.domain(d3.extent(data, d => d.events))
		.range([5, 15]);
	
	$: yScale = d3.scaleBand()
			.domain(hazards)
			.range([height - margin.bottom, margin.top]);
	
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

	// .tickFormat(d3.format("d"))
	
</script>

<svg {width} {height}>
	{#each data as d, i}
	{#if Object.hasOwn(d, 'description')}
			<text x={xScale(d.date)} y={yScale(d.hazard)+80} font-size=10 text-anchor='middle'>{d.description}</text>
		{/if}
		<circle
					cx={xScale(d.date)}
					r={sizeScale(d.events)}
					cy={yScale(d.hazard) + 55}
					fill={i === hovered ? "brown": Object.hasOwn(d, 'description') ? "red" : d3.color(coloroptions[d.hazard])}
					on:mouseover={(event) => 
					{ hovered = i; 
					  recorded_mouse_position = {
							x: event.pageX,
							y: event.pageY
						}}}
					on:mouseout={(event) => { hovered = -1; }} />
	{/each}
	
	<g transform="translate(0, {margin.bottom})"
		 bind:this={xAxis} />
	
	<g transform="translate({margin.left - 10}, 0)"
		 bind:this={yAxis} />
</svg>
<div
class={hovered === -1 ? "tooltip-hidden": "tooltip-visible"}
style="left: {recorded_mouse_position.x + 40}px; top: {recorded_mouse_position.y + 40}px"	
>
{#if hovered !== -1}
	{ data[hovered].events } {data[hovered].hazard}{ data[hovered].events===1 ? "" : "s" } in {data[hovered].date}.
{/if}
</div>


<style>
	/* svg {
		border: 2px dashed goldenrod;	
	} */
	
	circle {
		fill-opacity: 0.75;
		stroke: white;
	}

		/* dynamic classes for the tooltip */
		.tooltip-hidden {
		visibility: hidden;
		font-family: "Nunito", sans-serif;
		width: 200px;
		position: absolute;
	}

	.tooltip-visible {
		font: 15px sans-serif;
		font-family: "Nunito", sans-serif;
		visibility: visible;
		background-color: #f0dba8;
		border-radius: 10px;
		width: 100px;
		color: black;
		position: absolute;
		padding: 10px;
	}

	/* .annotate {
		border: 1px solid #ddd;
		box-shadow: 1px 1px 1px #ddd;
		background: white;
		border-radius: 4px;
		padding: 4px;
		position: absolute;
		font-size: 10px;
	} */


</style>