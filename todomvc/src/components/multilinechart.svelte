<script>
    // imports
    import { scaleLinear } from "d3-scale";

    // exports
    export let title = "";
    export let multipleData = {};
    // set general use variables
    let chartWidth = 600;
    let chartHeight = 200;

    const paddings = {
        top: 30,
        left: 150,
        right: 30,
        bottom: 30,
    };

    const centerX = chartWidth / 2;
    const centerY = chartHeight / 2;

    // set scaling variables
    $: xScale = scaleLinear()
        .domain([
            Math.min(
                ...[].concat(...Object.values(multipleData)).map((d) => d.index)
            ),
            Math.max(
                ...[].concat(...Object.values(multipleData)).map((d) => d.index)
            ),
        ])
        .range([paddings.left, chartWidth - paddings.right]);
    $: yScale = scaleLinear()
        .domain([
            Math.min(
                ...[].concat(...Object.values(multipleData)).map((d) => d.size)
            ),
            Math.max(
                ...[].concat(...Object.values(multipleData)).map((d) => d.size)
            ),
        ])
        .range([chartHeight - paddings.bottom, paddings.top]);

    // define tick marks
    let xTicks = [];
    let yTicks = [];
    let numTicks = 5;
    $: {
        xTicks = [];
        yTicks = [];

        if (Object.keys(multipleData).length > 0) {
            let index_extent = [
                Math.round(
                    Math.min(
                        ...[]
                            .concat(...Object.values(multipleData))
                            .map((d) => d.index)
                    )
                ),
                Math.round(
                    Math.max(
                        ...[]
                            .concat(...Object.values(multipleData))
                            .map((d) => d.index)
                    ) + 1
                ),
            ];
            let index_increment = Math.floor(
                (index_extent[1] - index_extent[0]) / numTicks
            );
            for (
                let i = index_extent[0];
                i < index_extent[1];
                i = i + Math.max(1, index_increment)
            ) {
                xTicks.push(i);
            }

            let size_extent = [
                Math.round(
                    Math.min(
                        ...[]
                            .concat(...Object.values(multipleData))
                            .map((d) => d.size)
                    )
                ),
                Math.round(
                    Math.max(
                        ...[]
                            .concat(...Object.values(multipleData))
                            .map((d) => d.size)
                    ) + 1
                ),
            ];
            let size_increment = Math.floor(
                (size_extent[1] - size_extent[0]) / numTicks
            );
            for (
                let i = size_extent[0];
                i < size_extent[1];
                i = i + Math.max(1, size_increment)
            ) {
                yTicks.push(i);
            }
        }
    }

    // hover effect
    const idContainer = "svg-container-" + Math.random() * 1000000;
    let mousePosition = { x: null, y: null };
    let pageMousePosition = { x: null, y: null };
    let currentHoveredPoint = null;

    function followMouse(event) {
        const svg = document.getElementById(idContainer);
        if (svg === null) return;
        const dim = svg.getBoundingClientRect();
        pageMousePosition = {
            x: event.pageX,
            y: event.pageY,
        };
        const positionInSVG = {
            x: event.clientX - dim.left,
            y: event.clientY - dim.top,
        };
        mousePosition =
            positionInSVG.x > paddings.left &&
            positionInSVG.x < chartWidth - paddings.right &&
            positionInSVG.y > paddings.top &&
            positionInSVG.y < chartHeight - paddings.bottom
                ? { x: positionInSVG.x, y: positionInSVG.y }
                : { x: null, y: null };
    }
    function removePointer() {
        mousePosition = { x: null, y: null };
    }

    function computeSelectedXValue(value) {
        currentHoveredPoint = [].concat(...Object.values(multipleData))[
            []
                .concat(...Object.values(multipleData))
                .indexOf(
                    []
                        .concat(...Object.values(multipleData))
                        .filter((d) => xScale(d.index) >= value)[0]
                ) - 1
        ];
        return (
            []
                .concat(...Object.values(multipleData))
                .filter((d) => xScale(d.index) >= value)[0].index - 1
        );
    }
</script>

<div class="visualization">
    <h4>{title}</h4>
    <svg
        width={chartWidth}
        height={chartHeight}
        viewBox={`0 0 ${chartWidth} ${chartHeight}`}
        on:mousemove={followMouse}
        on:mouseleave={removePointer}
        id={idContainer}
    >
        <g>
            <line
                x1={centerX - (chartWidth - paddings.left - paddings.right) / 2}
                x2={centerX + (chartWidth - paddings.left - paddings.right) / 2}
                y1={centerY +
                    (chartHeight - paddings.top - paddings.bottom) / 2}
                y2={centerY +
                    (chartHeight - paddings.top - paddings.bottom) / 2}
                stroke="#6e3003"
                stroke-width="2"
                class="axis"
            />
            <line
                x1={centerX - (chartWidth - paddings.left - paddings.right) / 2}
                x2={centerX - (chartWidth - paddings.left - paddings.right) / 2}
                y1={centerY +
                    (chartHeight - paddings.top - paddings.bottom) / 2}
                y2={centerY -
                    (chartHeight - paddings.top - paddings.bottom) / 2}
                stroke="#6e3003"
                stroke-width="2"
                class="axis"
            />
        </g>

        {#each Object.keys(multipleData) as key}
            <g>
                {#each multipleData[key] as d, i}
                    {#if i != multipleData[key].length - 1}
                        <line
                            x1={centerX -
                                (chartWidth - paddings.left - paddings.right) /
                                    2 +
                                xScale(multipleData[key][i].index) -
                                paddings.left}
                            x2={centerX -
                                (chartWidth - paddings.left - paddings.right) /
                                    2 +
                                xScale(multipleData[key][i + 1].index) -
                                paddings.left}
                            y1={centerY -
                                (chartHeight - paddings.top - paddings.bottom) /
                                    2 +
                                yScale(multipleData[key][i].size) -
                                paddings.top}
                            y2={centerY -
                                (chartHeight - paddings.top - paddings.bottom) /
                                    2 +
                                yScale(multipleData[key][i + 1].size) -
                                paddings.top}
                            stroke="#b86a04"
                            stroke-width="2"
                        />
                    {/if}
                {/each}
            </g>
        {/each}

        <g
            transform={`translate(0, ${
                centerY + (chartHeight - paddings.top - paddings.bottom) / 2
            })`}
        >
            {#each xTicks as x}
                <g
                    class="tick"
                    opacity="1"
                    transform={`translate(${
                        centerX -
                        (chartWidth - paddings.left - paddings.right) / 2 +
                        xScale(x) -
                        paddings.left
                    },0)`}
                >
                    <line stroke="#6e3003" y2="6" />
                    <text
                        class="tick-label"
                        dy="0.71em"
                        y="10"
                        x="-5"
                        text-anchor="middle"
                    >
                        {x}
                    </text>
                </g>
            {/each}
        </g>
        <g
            transform={`translate(${
                centerX - (chartWidth - paddings.left - paddings.right) / 2
            }, 0)`}
        >
            {#each yTicks as y}
                <g
                    class="tick"
                    opacity="1"
                    transform={`translate(0,${
                        centerY -
                        (chartHeight - paddings.top - paddings.bottom) / 2 +
                        yScale(y) -
                        paddings.top
                    })`}
                >
                    <line stroke="#6e3003" x2="-5" />
                    <text
                        class="tick-label"
                        dy="0.32em"
                        x="-{10}"
                        text-anchor="end"
                    >
                        {y}
                    </text>
                </g>
            {/each}
        </g>

        {#if mousePosition.x !== null}
            <g
                transform="translate({xScale(
                    computeSelectedXValue(mousePosition.x)
                )} 0)"
            >
                <line
                    x1="0"
                    x2="0"
                    y1={paddings.top}
                    y2={chartHeight - paddings.bottom - 2}
                    stroke="black"
                    stroke-width="1"
                />
                <circle
                    cx={0}
                    cy={yScale(
                        []
                            .concat(...Object.values(multipleData))
                            .find(
                                (d) =>
                                    d.index ===
                                    computeSelectedXValue(mousePosition.x)
                            ).size
                    )}
                    r="3"
                    fill="#b86a04"
                />
            </g>
        {/if}
    </svg>
    <div
        class={mousePosition.x === null ? "tooltip-hidden" : "tooltip-visible"}
        style="left: {pageMousePosition.x + 10}px; top: {pageMousePosition.y +
            10}px"
    >
        {#if mousePosition.x !== null}
            At index {currentHoveredPoint.index}, the size was {currentHoveredPoint.size}.
        {/if}
    </div>
    <div class="legend">
        {#each Object.keys(multipleData) as key, i}
            <div class="legend-item">
                <span
                    class="legend-color"
                    style="background-color: {i === 0 ? '#b86a04' : '#6e3003'}"
                />
                <span class="legend-text">{key}</span>
            </div>
        {/each}
    </div>
</div>

<style>
    .visualization {
        font: 25px sans-serif;
        margin: auto;
        margin-top: 1px;
        text-align: center;
    }

    /* dynamic classes for the tooltip */
    .tooltip-hidden {
        visibility: hidden;
        font-family: "Nunito", sans-serif;
        width: 200px;
        position: absolute;
    }

    .tooltip-visible {
        font: 25px sans-serif;
        font-family: "Nunito", sans-serif;
        visibility: visible;
        background-color: #f0dba8;
        border-radius: 10px;
        width: 200px;
        color: black;
        position: absolute;
        padding: 10px;
    }

    .axis {
        stroke-linejoin: round;
        stroke-dasharray: 4400;
        stroke-dashoffset: 0;
        /* animation: draw 8.5s ease; */
    }

    .tick-label {
        font-size: 12px;
        fill: #6e3003;
    }

    .legend {
        display: flex;
        flex-wrap: wrap;
        margin-top: 10px;
        justify-content: center;
    }

    .legend-item {
        display: flex;
        align-items: center;
        margin-right: 10px;
    }

    .legend-color {
        display: inline-block;
        width: 20px;
        height: 20px;
        margin-right: 5px;
    }
</style>
