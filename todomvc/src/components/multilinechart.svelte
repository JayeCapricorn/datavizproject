<script>
    // imports
    import { scaleLinear } from "d3-scale";

    // exports
    export let title = "";
    export let multipleData = {};
    // set general use variables
    let chartWidth = 400;
    let chartHeight = 200;

    const paddings = {
        top: 50,
        left: 100,
        right: 50,
        bottom: 50,
    };

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

        console.log(multipleData);

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
        on:mousemove={followMouse}
        on:mouseleave={removePointer}
        id={idContainer}
    >
        <g>
            <line
                x1={paddings.left}
                x2={chartWidth - paddings.right}
                y1={chartHeight - paddings.bottom}
                y2={chartHeight - paddings.bottom}
                stroke="#6e3003"
                stroke-width="2"
                class="axis"
            />
            <line
                x1={paddings.left}
                x2={paddings.left}
                y1={chartHeight - paddings.bottom}
                y2={paddings.top}
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
                            x1={xScale(multipleData[key][i].index)}
                            x2={xScale(multipleData[key][i + 1].index)}
                            y1={yScale(multipleData[key][i].size)}
                            y2={yScale(multipleData[key][i + 1].size)}
                            stroke="#b86a04"
                            stroke-width="2"
                        />
                    {/if}
                {/each}
            </g>
        {/each}

        <g transform="translate(0, {chartHeight - paddings.bottom})">
            {#each xTicks as x}
                <g
                    class="tick"
                    opacity="1"
                    transform="translate({xScale(x)},0)"
                >
                    <line stroke="#6e3003" y2="6" />
                    <text
                        dy="0.71em"
                        fill="#6e3003"
                        y="10"
                        x="-5"
                        text-anchor="middle"
                    >
                        {x}
                    </text>
                </g>
            {/each}
        </g>
        <g transform="translate({paddings.left}, 0)">
            {#each yTicks as y}
                <g
                    class="tick"
                    opacity="1"
                    transform="translate(0,{yScale(y)})"
                >
                    <line stroke="#6e3003" x2="-5" />
                    <text
                        dy="0.32em"
                        fill="#6e3003"
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
        text-align: middle;
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

    .legend {
        display: flex;
        flex-wrap: wrap;
        margin-top: 10px;
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
