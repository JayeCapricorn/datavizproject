<script>
    export let index;
    import Barchart from "./barchart.svelte";
    import Scatterplot from "./scatterplot.svelte";
    import Linechart from "./linechart.svelte";
    import Multilinechart from "./multilinechart.svelte";
    import Wordcloud from "./wordcloud.svelte";

    import migration_line_data from "../data/migration_line.json";
    import owid_data from "../data/owid.json";
    import disaster_migration_scatter_data from "../data/disaster_migration_scatter.json";
    import disaster_indicator_scatter_data from "../data/disaster_indicator_scatter.json";

    let migration_line_data_processed = [];
    migration_line_data.forEach((element) =>
        migration_line_data_processed.push({
            index: element["year"],
            size: element["value"],
        })
    );

    let owid_data_processed = {};
    // do what we did for migration line data, except for each country in a dictionary by iterating over the keys in owid_data
    Object.entries(owid_data).forEach(([type, type_data]) => {
        Object.entries(type_data).forEach(([country, country_data]) => {
            if (country_data.length > 0) {
                if (!(type in owid_data_processed)) {
                    owid_data_processed[type] = {};
                }
                owid_data_processed[type][country] = [];
                country_data.forEach((element) =>
                    owid_data_processed[type][country].push({
                        index: element["year"],
                        size: element["value"],
                    })
                );
            }
        });
    });

    let disaster_migration_scatter_data_processed = [];
    disaster_migration_scatter_data["data"].forEach((element) =>
        disaster_migration_scatter_data_processed.push({
            x: element["disaster"],
            y: element["migration"],
            color: element["country"],
        })
    );

    const indicator_descs = {
        "FB.CBK.BRWR.P3": "Borrowers From Commercial Banks",
        "FP.WPI.TOTL": "Wholesale Price Index 3 Years After The Disaster",
        "FP.CPI.TOTL": "Consumer Price Index 3 Years After The Disaster",
        "SN.ITK.SVFI.ZS": "Prevalence of Severe Food Insecurity In The Population (%) 3 Years After The Disaster",
    };
    let disaster_indicator_scatter_data_processed = {};
    Object.entries(disaster_indicator_scatter_data).forEach(
        ([indicator, indicator_data]) => {
            disaster_indicator_scatter_data_processed[indicator] = [];
            indicator_data["data"].forEach((element) =>
                disaster_indicator_scatter_data_processed[indicator].push({
                    x: element["disaster"],
                    y: element["indicator"],
                    color: element["country"],
                })
            );
        }
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
        <!-- Bind "Number of deaths from disasters" and "Number of people left homeless from disasters" using a for loop -->
        {#each Object.keys(owid_data_processed) as type}
            <Multilinechart
                bind:multipleData={owid_data_processed[type]}
                bind:title={type}
            />
        {/each}
        <!-- <Scatterplot /> -->
        <!-- <img src="/images/bgmap.jpg" alt="background image" class="center"/> -->
    {:else if index == 2}
        <Scatterplot
            bind:data={disaster_migration_scatter_data_processed}
            bind:ols={disaster_migration_scatter_data["ols"]}
        />
        <!-- <img src="/images/map_index.jpg" alt="background image" class="center"/> -->
    {:else if index == 3}
        <Wordcloud />
    {:else if index == 4}
        <Scatterplot
            bind:data={disaster_indicator_scatter_data_processed[
                "FB.CBK.BRWR.P3"
            ]}
            bind:ols={disaster_indicator_scatter_data["FB.CBK.BRWR.P3"]["ols"]}
            bind:title={indicator_descs["FB.CBK.BRWR.P3"]}
        />
        <Scatterplot
            bind:data={disaster_indicator_scatter_data_processed["FP.WPI.TOTL"]}
            bind:ols={disaster_indicator_scatter_data["FP.WPI.TOTL"]["ols"]}
            bind:title={indicator_descs["FP.WPI.TOTL"]}
        />
        <Scatterplot
            bind:data={disaster_indicator_scatter_data_processed["FP.CPI.TOTL"]}
            bind:ols={disaster_indicator_scatter_data["FP.CPI.TOTL"]["ols"]}
            bind:title={indicator_descs["FP.CPI.TOTL"]}
        />
    {:else if index == 5}
        <Scatterplot
            bind:data={disaster_indicator_scatter_data_processed["SN.ITK.SVFI.ZS"]}
            bind:ols={disaster_indicator_scatter_data["SN.ITK.SVFI.ZS"]["ols"]}
            bind:title={indicator_descs["SN.ITK.SVFI.ZS"]}
        />
    {:else}
        <Barchart />
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
