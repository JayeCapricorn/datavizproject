<script>
    export let index;
    import Barchart from "./barchart.svelte";
    import Scatterplot from "./scatterplot.svelte";
    import Multilinechart from "./multilinechart.svelte";
    import Wordcloudecon from "./wordcloudecon.svelte";
    import Wordcloudfood from "./wordcloudfood.svelte";

    import migration_line_data from "../data/migration_line.json";
    import owid_data from "../data/owid.json";
    import disaster_migration_scatter_data from "../data/disaster_migration_scatter.json";
    import disaster_indicator_scatter_data from "../data/disaster_indicator_scatter.json";
    import indicator_migration_scatter_data from "../data/indicator_migration_scatter.json";
    import ext_mig_factors_data from "../data/ext_mig_factors.json";
    import int_mig_factors_data from "../data/int_mig_factors.json";

    let migration_line_data_processed = {};
    Object.entries(migration_line_data).forEach(([country, country_data]) => {
        migration_line_data_processed[country] = [];
        country_data.forEach((element) =>
            migration_line_data_processed[country].push({
                index: element["year"],
                size: element["value"],
            })
        );
    });

    let owid_data_processed = {};
    let owid_types = {};
    // do what we did for migration line data, except for each country in a dictionary by iterating over the keys in owid_data
    Object.entries(owid_data).forEach(([type, type_data]) => {
        owid_types[type] = type;
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
    disaster_migration_scatter_data["SM.POP.NETM"]["data"].forEach((element) =>
        disaster_migration_scatter_data_processed.push({
            x: element["disaster"],
            y: element["indicator"],
            country: element["country"],
        })
    );

    const indicator_descs = {
        "FB.CBK.BRWR.P3": "Borrowers From Commercial Banks",
        "FP.WPI.TOTL": "Wholesale Price Index 3 Years After The Disaster",
        "FP.CPI.TOTL": "Consumer Price Index 3 Years After The Disaster",
        "SN.ITK.SVFI.ZS":
            "Prevalence of Severe Food Insecurity In The Population (%) 3 Years After The Disaster",
    };
    let disaster_indicator_scatter_data_processed = {};
    Object.entries(disaster_indicator_scatter_data).forEach(
        ([indicator, indicator_data]) => {
            disaster_indicator_scatter_data_processed[indicator] = [];
            indicator_data["data"].forEach((element) =>
                disaster_indicator_scatter_data_processed[indicator].push({
                    x: element["disaster"],
                    y: element["indicator"],
                    country: element["country"],
                })
            );
        }
    );

    let indicator_migration_scatter_data_processed = {};
    Object.entries(indicator_migration_scatter_data).forEach(
        ([indicator, indicator_data]) => {
            indicator_migration_scatter_data_processed[indicator] = [];
            indicator_data["data"].forEach((element) =>
                indicator_migration_scatter_data_processed[indicator].push({
                    x: element["indicator"],
                    y: element["migration"],
                    country: element["country"],
                })
            );
        }
    );

    let ext_mig_factors_data_processed = [];
    ext_mig_factors_data.forEach((element) =>
        ext_mig_factors_data_processed.push({
            type: element["desc"],
            value: element["weight"],
            highlight: element["highlight"],
        })
    );

    let int_mig_factors_data_processed = [];
    int_mig_factors_data.forEach((element) =>
        int_mig_factors_data_processed.push({
            type: element["desc"],
            value: element["weight"],
            highlight: element["highlight"],
        })
    );

    let isVisible = true;

</script>

<main class:visible={isVisible}>
    {#if index == 0}
        <Multilinechart
            bind:multipleData={owid_data_processed[
                "Number of deaths from disasters"
            ]}
            bind:title={owid_types["Number of deaths from disasters"]}
        />
        <!-- <Multilinechart
            bind:multipleData={owid_data_processed[
                "Number of people left homeless from disasters"
            ]}
            bind:title={owid_types[
                "Number of people left homeless from disasters"
            ]}
        /> -->
        <Multilinechart
            bind:multipleData={owid_data_processed[
                "Number of total people affected by disasters"
            ]}
            bind:title={owid_types[
                "Number of total people affected by disasters"
            ]}
        />
    {:else if index == 1}
        <Multilinechart 
        bind:multipleData={migration_line_data_processed} 
        title="Net Migration"
        />
    {:else if index == 2}
        <Scatterplot
            bind:data={disaster_migration_scatter_data_processed}
            bind:ols={disaster_migration_scatter_data["SM.POP.NETM"]["ols"]}
        />
    {:else if index == 3}
        <Wordcloudecon />
    {:else if index == 4}
        <Multilinechart
            bind:multipleData={owid_data_processed[
                "Total economic damages from disasters"
            ]}
            bind:title={owid_types["Total economic damages from disasters"]}
        />
    {:else if index == 5}
        <Scatterplot
            bind:data={disaster_indicator_scatter_data_processed[
                "FB.CBK.BRWR.P3"
            ]}
            bind:ols={disaster_indicator_scatter_data["FB.CBK.BRWR.P3"]["ols"]}
            bind:title={indicator_descs["FB.CBK.BRWR.P3"]}
        />
    {:else if index == 6}
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
    {:else if index == 7}
        <Scatterplot
            bind:data={indicator_migration_scatter_data_processed[
                "FP.WPI.TOTL"
            ]}
            bind:ols={indicator_migration_scatter_data["FP.WPI.TOTL"]["ols"]}
        />
        <Barchart bind:data={ext_mig_factors_data_processed} />
    {:else if index == 8}
        <Wordcloudfood />
    {:else if index == 9}
        <Scatterplot
            bind:data={disaster_indicator_scatter_data_processed[
                "SN.ITK.SVFI.ZS"
            ]}
            bind:ols={disaster_indicator_scatter_data["SN.ITK.SVFI.ZS"]["ols"]}
            bind:title={indicator_descs["SN.ITK.SVFI.ZS"]}
        />
    {:else}
        <Barchart bind:data={int_mig_factors_data_processed} />
    {/if}
</main>

<style>
    /* .img2 {
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
    } */
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
        position:relative;
        /* border:5px solid; */
        top: 45%;
        transform: translate(0, -50%);
    }
</style>
