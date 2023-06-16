<script>
    // import {gt_volcano} from '../data/distributiondata.js';
    import * as d3 from "d3";

    // let data = gt_volcano;
    export let data;
    export let margin;
    export let color;

    let width = 1000;
    let height = 1900;
    // let margin = { top: 10, bottom: 40, left: 870, right: 20 };

    // $: xScale = d3.scaleLinear()
    // 	.domain([1960, 2022])
    // 	.range([margin.left, width - margin.right]);
    $: xScale = d3
        .scaleLinear()
        .domain([0, 0.2])
        .range([margin.left, width - margin.right]);

    // $: yScale = d3.scaleLinear()
    // 	.domain([0, 0.2])
    // 	.range([height - margin.bottom, margin.top]);
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
            .attr("dy", "0.35em")
            .attr("dx", "-1em")
            .attr("text-anchor", "end")
            .attr("transform", "rotate(-90)");
    }
</script>

<!-- rotate(90) -->

<svg {width} {height} transform="translate({margin.left}, {margin.top})">
    <g>
        {#each data as d, i}
            {#if i != data.length - 1}
                <line
                    x1={xScale(data[i][1]) + 20}
                    x2={xScale(data[i + 1][1]) + 20}
                    y1={yScale(data[i][0])}
                    y2={yScale(data[i + 1][0])}
                    stroke={color}
                    stroke-width="1"
                />
            {/if}
        {/each}
    </g>

    <!-- stroke="#b86a04" -->
    <!-- <g transform="translate(0, {height - margin.bottom})"
		 bind:this={xAxis} /> -->

    <!-- <g transform="translate({margin.left}, 0)"
		 bind:this={yAxis} /> -->
</svg>

<style></style>
