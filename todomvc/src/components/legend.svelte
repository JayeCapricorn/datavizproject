<script>
	export let margin;
	import * as d3 from "d3";
	import { legendSize } from "d3-svg-legend";

	$: legendScale = d3.scaleSqrt().domain([0, 100000, 1000000]).range([5, 10]);

	let legend;

	$: {
		const colorLegend = legendSize()
			.shape("circle")
			.scale(legendScale)
			.shapePadding(50)
			.labelOffset(20)
			.orient("horizontal")
			.title("People affected")
			.cells(3)
			.labelFormat(d3.format(","));

		d3.select(legend).call(colorLegend);
	}
</script>

<g transform="translate(20, {margin.top + 3})" bind:this={legend} />

<style>
</style>
