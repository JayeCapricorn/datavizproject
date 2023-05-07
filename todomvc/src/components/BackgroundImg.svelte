<script>
    export let index;
    import Barchart from "./barchart.svelte";
    import Scatterplot from "./scatterplot.svelte";
    import Linechart from "./linechart.svelte";

    import migration_line_data from "../data/migration_line.json";

    let migration_line_data_processed = [];
    migration_line_data.forEach((element) =>
    migration_line_data_processed.push({
            index: element["year"],
            size: element["value"],
        })
    );

    let isVisible = true;
</script>

<main class:visible={isVisible}>
    <!-- <img src={testurls[index]} alt="background image" class="center"/> -->
    {#if index == 0}
        <!-- <img src="/images/image.png" class="img2"/>
    <img src="/images/imgtest.PNG" class="img3"/> -->
        <Linechart bind:data={migration_line_data_processed} />
    {:else if index == 1}
        <Scatterplot />
        <!-- <img src="/images/bgmap.jpg" alt="background image" class="center"/> -->
    {:else}
        <Barchart />
        <!-- <img src="/images/map_index.jpg" alt="background image" class="center"/> -->
    {/if}
</main>

<style>
    .img2 {
        z-index: 3;
        position: absolute;
        left: 150px;
        width: 20%;
    }
    .img3 {
        z-index: 3;
        position: absolute;
        right: 200px;
        top: 80px;
        width: 20%;
    }

    .center {
        display: block;
        top: 80px;
        margin-left: auto;
        margin-right: auto;
        width: 85%;
        height: 85%;
    }
    main {
        /* width: 100%;
    height: 100vh;
    position: absolute; */
        opacity: 0;
        visibility: hidden;
    }

    main.visible {
        opacity: 1;
        visibility: visible;
    }
</style>
