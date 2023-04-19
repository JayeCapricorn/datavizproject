<script>
	import * as d3 from 'd3';
	import {onMount} from 'svelte';
	import Testline from '../components/testline.svelte';
	import Eventline from './eventline.svelte';
	import Legend from './legend.svelte';
	import {gt_volcano, gt_earthquakes, gt_drought, gt_floods, gt_landslide, gt_storm,
	        hn_drought, hn_earthquakes, hn_floods, hn_storm, 
		elsl_drought, elsl_earthquakes, elsl_floods, elsl_landslide, elsl_storm, elsl_volcano} from '../data/distributiondata.js';
	export let data;
	export let menu; 
	
    let hazards = ["Flood", "Storm", "Drought", "Landslide", "Earthquake", "Volcanic activity"];
	let coloroptions = {"Earthquake": "#E3963E", "Flood" : "#3D85C6", "Storm": "teal", "Volcanic activity": "#E97451", "Drought": "gray", "Landslide": "#6F4E37"};
	let hovered = -1; 
	let recorded_mouse_position = {
		x: 0, y: 0
	};
	
	let width = 1000;
	let height = 2000;
	
	let margin = {top: 10, right: 50, bottom: 150, left: 50};
	let margin6 = { top: 10, bottom: 40, left: 870, right: 50 };
	let margin5 = { top: 10, bottom: 40, left: 710, right: 100 };
	let margin4 = { top: 10, bottom: 40, left: 570, right: 360 };
	let margin3 = { top: 10, bottom: 40, left: 410, right: 480 };
	let margin2 = { top: 10, bottom: 40, left: 260, right: 500 };
	let margin1 = { top: 10, bottom: 40, left: 120, right: 650 };

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

<svg width="500" height="90" font-family="Nunito" font-size="10px" fill-opacity=0.5>
	<Legend margin={margin}/>
</svg>

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

		{#if d.hasOwnProperty('Description')}
		<Eventline x1={margin.left - 40} x2={xScale(d.DisasterType) + 80} y1={yScale(d.Year)} y2={yScale(d.Year)}/>
			{/if}
	{/each}

	{#if menu === 1}
	<Testline data={gt_volcano} margin={margin6} color="#E97451"/>
	<Testline data={gt_earthquakes} margin={margin5} color="#E3963E"/>
	<Testline data={gt_landslide} margin={margin4} color="#6F4E37"/>
	<Testline data={gt_drought} margin={margin3} color="gray"/>
	<Testline data={gt_storm} margin={margin2} color="teal"/>
	<Testline data={gt_floods} margin={margin1} color="#3D85C6"/>
	{:else if menu === 2}
	<Testline data={hn_earthquakes} margin={margin5} color="#E3963E"/>
	<Testline data={hn_drought} margin={margin3} color="gray"/>
	<Testline data={hn_storm} margin={margin2} color="teal"/>
	<Testline data={hn_floods} margin={margin1} color="#3D85C6"/>
	{:else if menu === 3}
	<Testline data={elsl_volcano} margin={margin6} color="#E97451"/>
	<Testline data={elsl_earthquakes} margin={margin5} color="#E3963E"/>
	<Testline data={elsl_landslide} margin={margin4} color="#6F4E37"/>
	<Testline data={elsl_drought} margin={margin3} color="gray"/>
	<Testline data={elsl_storm} margin={margin2} color="teal"/>
	<Testline data={elsl_floods} margin={margin1} color="#3D85C6"/>
	{/if}
	
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
	style="left: {90}px; top: {yScale(d.Year) + 90}px"	
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
		width: 140px;
		position: absolute;
	}

	.tooltip-visible {
		font: 14px sans-serif;
		font-family: "Nunito", sans-serif;
		visibility: visible;
		background-color: #f0dba8;
		border-radius: 10px;
		width: 140px;
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
		width: 80px;
		color: black;
		position: absolute;
		padding: 10px;
	}

</style>