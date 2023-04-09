<script>
	import * as d3 from 'd3';
	import {onMount} from 'svelte';
	export let data;
	// export let color;
	export let eventname;
	
	let coloroptions = {"earthquake": "orange", "flood" : "blue", "cyclone": "teal", "eruption": "red"};
	let hovered = -1; 
	let recorded_mouse_position = {
		x: 0, y: 0
	};

	let color = d3.color(coloroptions[eventname]);
	
	let width = 950;
	let height = 100;
	
	let margin = {top: 10, right: 10, bottom: 25, left: 20};
	
	
	// $: xScale = d3.scalePoint()
	// 	.domain(data.map(d => d.date))
	// 	.range([margin.left, width - margin.right]);
	$: xScale = d3.scaleLinear()
		.domain([1539, 2022])
		.range([margin.left, width - margin.right]);

	$: sizeScale = d3.scaleSqrt()
		.domain(d3.extent(data, d => d.events))
		.range([5, 10]);
	
	// $: yScale = d3.scaleLinear()
	// 		.domain([0, d3.max(data, d => d.earthquakes)])
	// 		.range([height - margin.bottom, margin.top])
	
	let xAxis;
	// let yAxis;
	
	$: {
		// d3.select(yAxis).call(d3.axisLeft(yScale));
		
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
		<circle
					cx={xScale(d.date)}
					r={sizeScale(d.events)}
					cy={10}
					fill={i === hovered ? "brown": color}
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
	
	<!-- <g transform="translate({margin.left}, 0)"
		 bind:this={yAxis} /> -->
</svg>
<div
class={hovered === -1 ? "tooltip-hidden": "tooltip-visible"}
style="left: {recorded_mouse_position.x + 40}px; top: {recorded_mouse_position.y + 40}px"	
>
{#if hovered !== -1}
	{ data[hovered].events } {eventname}{ data[hovered].events===1 ? "" : "s" } in {data[hovered].date}.
{/if}
</div>


<style>
	/* svg {
		border: 2px dashed goldenrod;	
	} */
	
	circle {
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


</style>