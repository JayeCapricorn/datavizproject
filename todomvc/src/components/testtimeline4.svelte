<script>
	import * as d3 from 'd3';
	import {onMount} from 'svelte';
	export let data;
	
    let hazards = ["Flood", "Storm", "Drought", "Landslide", "Earthquake", "Volcanic activity"];
	let coloroptions = {"Earthquake": "#E3963E", "Flood" : "#3D85C6", "Storm": "teal", "Volcanic activity": "#E97451", "Drought": "gray", "Landslide": "#6F4E37"};
	let hovered = -1; 
	let recorded_mouse_position = {
		x: 0, y: 0
	};
	
	let width = 1000;
	let height = 2000;
	
	let margin = {top: 10, right: 50, bottom: 150, left: 50};

    $: xScale = d3.scaleBand()
			.domain(hazards)
			.range([margin.left, width - margin.right]);

	$: sizeScale = d3.scaleSqrt()
		.domain(d3.extent(data, d => d.TotalAffected))
		.range([10, 25]);

    $: yScale = d3.scaleLinear()
		.domain([1960, 2022])
		.range([margin.top, height - margin.bottom]);
	
	let xAxis;
	let yAxis;
	
	$: {
		d3.select(yAxis).call(d3.axisLeft(yScale));
		
		d3.select(xAxis)
				.call(d3.axisBottom(xScale))
				.selectAll('.tick > text')
				.attr('y', 0)
				.attr('dy', '-1em')
				.attr('dx', '-1em')
				.attr('text-anchor', 'end')
				.attr('transform', 'rotate(-360)');

	}

	// .tickFormat(d3.format("d"))
	
</script>

<svg {width} {height}>
	{#each data as d, i}
		<circle
					cx={xScale(d.DisasterType) + 80}
					r={d.TotalAffected === '' ? 5 : sizeScale(d.TotalAffected)}
                    cy={yScale(d.Year)}
					height={yScale(1900)-yScale(d.Year)}
					fill={i === hovered ? "purple": d.hasOwnProperty('Description') ? "black" : d3.color(coloroptions[d.DisasterType])}
					on:mouseover={(event) => 
					{ hovered = i; 
					  recorded_mouse_position = {
							x: event.pageX,
							y: event.pageY
						}}}
					on:mouseout={(event) => { hovered = -1; }} />
	{/each}
	
	<g transform="translate(0, {margin.bottom-130})"
		 bind:this={xAxis} />
	
	<g transform="translate({margin.left - 10}, 0)"
		 bind:this={yAxis} />
</svg>
<div
class={hovered === -1 ? "tooltip-hidden": "tooltip-visible"}
style="left: {recorded_mouse_position.x + 40}px; top: {recorded_mouse_position.y + 40}px"	
>
{#if hovered !== -1}
<p> {data[hovered].DisasterType} in {data[hovered].Year}. <br>
	{#if data[hovered].TotalAffected !== ''}
	Total Affected: {(data[hovered].TotalAffected).toLocaleString()}<br>
	{/if}
	{#if data[hovered].TotalDamages !== ''}
	Total Damages: ${(data[hovered].TotalDamages).toLocaleString()}
	{/if}
	</p>
{/if}
</div>

{#each data as d, i}
    {#if d.hasOwnProperty('Description')}
	<div
	class="window"
	style="left: {xScale(d.DisasterType) + 125}px; top: {yScale(d.Year) + 40}px"	
	>
	{d.Description}
	</div>
		{/if}
{/each}


<style>
	
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
		width: 150px;
		color: black;
		position: absolute;
		padding: 10px;
        z-index: 9;
	}

	.window {
		font: 10px sans-serif;
		font-family: "Nunito", sans-serif;
		visibility: visible;
		background-color: #f0c4a8;
		border-radius: 10px;
		width: 100px;
		color: black;
		position: absolute;
		padding: 10px;
	}

</style>