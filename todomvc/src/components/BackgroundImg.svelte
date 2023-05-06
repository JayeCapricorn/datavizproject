<script>
    export let index;
    import Barchart from "./barchart.svelte";
    import Scatterplot from "./scatterplot.svelte";
    import Linechart from "./linechart.svelte";

    import { weddings } from "../data/weddings";

    let weddings_data = [];
    weddings.forEach((element) =>
        weddings_data.push({
            index: element["Year"],
            size: element["Civil"],
        })
    );

    let isVisible = true;
</script>

<main class:visible={isVisible}>
    <!-- <img src={testurls[index]} alt="background image" class="center"/> -->
    {#if index == 0}
        <!-- <img src="/images/image.png" class="img2"/>
    <img src="/images/imgtest.PNG" class="img3"/> -->
        <Barchart />
    {:else if index == 1}
        <Scatterplot />
        <!-- <img src="/images/bgmap.jpg" alt="background image" class="center"/> -->
    {:else}
        <Linechart bind:data={weddings_data} />
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
