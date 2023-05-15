<script>
	import * as d3 from "d3";
	import Distributionline from "./distributionline.svelte";
	import Eventline from "./eventline.svelte";
	import Legend from "./legend.svelte";
	import {
		gt_volcano,
		gt_earthquakes,
		gt_drought,
		gt_floods,
		gt_landslide,
		gt_storm,
		hn_drought,
		hn_earthquakes,
		hn_floods,
		hn_storm,
		elsl_drought,
		elsl_earthquakes,
		elsl_floods,
		elsl_landslide,
		elsl_storm,
		elsl_volcano,
		all_volcano,
		all_earthquakes,
		all_drought,
		all_floods,
		all_landslide,
		all_storm,
	} from "../data/distributiondata.js";
	export let data;
	export let menu;

	let hazards = [
		"Flood",
		"Storm",
		"Drought",
		"Landslide",
		"Earthquake",
		"Volcanic activity",
	];
	let coloroptions = {
		Earthquake: "#E3963E",
		Flood: "#3D85C6",
		Storm: "teal",
		"Volcanic activity": "#E97451",
		Drought: "gray",
		Landslide: "#6F4E37",
	};
	let hovered = -1;
	let recorded_mouse_position = {
		x: 0,
		y: 0,
	};

	let width = 1000;
	let height = 2000;

	let margin = { top: 10, right: 50, bottom: 150, left: 50 };
	let margin6 = { top: 10, bottom: 40, left: 870, right: 50 };
	let margin5 = { top: 10, bottom: 40, left: 710, right: 100 };
	let margin4 = { top: 10, bottom: 40, left: 570, right: 360 };
	let margin3 = { top: 10, bottom: 40, left: 410, right: 480 };
	let margin2 = { top: 10, bottom: 40, left: 260, right: 500 };
	let margin1 = { top: 10, bottom: 40, left: 120, right: 650 };

	$: xScale = d3
		.scaleBand()
		.domain(hazards)
		.range([margin.left, width - margin.right]);

	$: sizeScale = d3
		.scaleSqrt()
		.domain(d3.extent(data, (d) => d.TotalAffected))
		.range([10, 25]);

	$: yScale = d3
		.scaleLinear()
		.domain([1960, 2022])
		.range([margin.top, height - margin.bottom]);

	let xAxis;
	let yAxis;

	$: {
		d3.select(yAxis).call(d3.axisLeft(yScale));

		d3.select(xAxis)
			.call(d3.axisBottom(xScale))
			.selectAll(".tick > text")
			.attr("y", 0)
			.attr("dy", "-1em")
			.attr("dx", "-1em")
			.attr("text-anchor", "end")
			.attr("font-size", "11px")
			.attr("transform", "rotate(-360)");
		d3.select(xAxis)
			.selectAll(".tick > text")
			.attr("transform", "translate(25, 0)");
		d3.select(xAxis)
			.selectAll(".domain")
			.style("stroke-width", "0px");
		d3.select(yAxis)
		.selectAll(".domain")
		.style("stroke-width", "0px");

		}
	

	// .tickFormat(d3.format("d"))
</script>

<svg
	width="200"
	height="90"
	font-family="Nunito"
	font-size="10px"
	fill-opacity="0.5"
>
	<Legend {margin} />
</svg>

<br />

<div style="position: relative;">
	<svg {width} {height}>
		{#each data as d, i}
			<circle
				cx={xScale(d.DisasterType) + 80}
				r={d.TotalAffected === "" ? 5 : sizeScale(d.TotalAffected)}
				cy={yScale(d.Year)}
				height={yScale(1900) - yScale(d.Year)}
				fill={i === hovered
					? "purple"
					: d3.color(coloroptions[d.DisasterType])}
				on:mouseover={(event) => {
					hovered = i;
					recorded_mouse_position = {
						x: event.pageX,
						y: yScale(d.Year),
					};
				}}
				on:mouseout={(event) => {
					hovered = -1;
				}}
			/>

			{#if d.hasOwnProperty("Description")}
				<Eventline
					x1={0}
					x2={xScale(d.DisasterType) + 80}
					y1={yScale(d.Year)}
					y2={yScale(d.Year)}
				/>
			{/if}
		{/each}

		{#if menu === 1}
			<Distributionline
				data={gt_volcano}
				margin={margin6}
				color="#E97451"
			/>
			<Distributionline
				data={gt_earthquakes}
				margin={margin5}
				color="#E3963E"
			/>
			<Distributionline
				data={gt_landslide}
				margin={margin4}
				color="#6F4E37"
			/>
			<Distributionline data={gt_drought} margin={margin3} color="gray" />
			<Distributionline data={gt_storm} margin={margin2} color="teal" />
			<Distributionline
				data={gt_floods}
				margin={margin1}
				color="#3D85C6"
			/>
		{:else if menu === 2}
			<Distributionline
				data={hn_earthquakes}
				margin={margin5}
				color="#E3963E"
			/>
			<Distributionline data={hn_drought} margin={margin3} color="gray" />
			<Distributionline data={hn_storm} margin={margin2} color="teal" />
			<Distributionline
				data={hn_floods}
				margin={margin1}
				color="#3D85C6"
			/>
		{:else if menu === 3}
			<Distributionline
				data={elsl_volcano}
				margin={margin6}
				color="#E97451"
			/>
			<Distributionline
				data={elsl_earthquakes}
				margin={margin5}
				color="#E3963E"
			/>
			<Distributionline
				data={elsl_landslide}
				margin={margin4}
				color="#6F4E37"
			/>
			<Distributionline
				data={elsl_drought}
				margin={margin3}
				color="gray"
			/>
			<Distributionline data={elsl_storm} margin={margin2} color="teal" />
			<Distributionline
				data={elsl_floods}
				margin={margin1}
				color="#3D85C6"
			/>
		{:else if menu === 4}
			<Distributionline
				data={all_volcano}
				margin={margin6}
				color="#E97451"
			/>
			<Distributionline
				data={all_earthquakes}
				margin={margin5}
				color="#E3963E"
			/>
			<Distributionline
				data={all_landslide}
				margin={margin4}
				color="#6F4E37"
			/>
			<Distributionline
				data={all_drought}
				margin={margin3}
				color="gray"
			/>
			<Distributionline data={all_storm} margin={margin2} color="teal" />
			<Distributionline
				data={all_floods}
				margin={margin1}
				color="#3D85C6"
			/>
		{/if}

		<g transform="translate(0, {margin.bottom - 130})" bind:this={xAxis} />

		<g transform="translate({margin.left - 10}, 0)" bind:this={yAxis} />
	</svg>
	<div
		class={hovered === -1 ? "tooltip-hidden" : "tooltip-visible"}
		style="left: {recorded_mouse_position.x +
			10}px; top: {recorded_mouse_position.y + 10}px"
	>
		{#if hovered !== -1}
			<p>
				{data[hovered].DisasterType} in {data[hovered].Year}. <br />
				{#if data[hovered].TotalAffected !== ""}
					Total Affected: {data[
						hovered
					].TotalAffected.toLocaleString()}<br />
				{/if}
				{#if data[hovered].TotalDamages !== ""}
					Total Damages: ${data[
						hovered
					].TotalDamages.toLocaleString()}
				{/if}
			</p>
		{/if}
	</div>

	{#each data as d, i}
		{#if d.hasOwnProperty("Description")}
			<div
				class="window"
				style="left: calc(50% - 620px); top: {yScale(
					d.Year
				)}px; transform: translateY(-50%)"
			>
				{#if d.hasOwnProperty("Imageurl")}
					<img src={d.Imageurl} style="width: 80%" />
				{/if}
				{d.Description}
			</div>
		{/if}
	{/each}
</div>

<style>
	circle {
		fill-opacity: 0.7;
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
		background-color: #ededed;
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
		background-color: #ffffff;
		outline: rgb(197, 197, 197) dashed 0.5px;
		width: 80px;
		color: black;
		position: absolute;
		padding: 10px;
	}


</style>
