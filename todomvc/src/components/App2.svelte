<script>
	import Testtimeline2 from '../components/testtimeline2.svelte';
    import Testtimeline3 from './testtimeline3.svelte';
	import { gt_earthquakes, hn_earthquakes, elsl_earthquakes, gt_floods, hn_floods, elsl_floods,
	         gt_cyclones, hn_cyclones, elsl_cyclones, gt_volcano, elsl_volcano } from "../data/timelinedata2";

	export let menu = 1;
    
    let gt_data = [];
	let gt_1 = gt_earthquakes.map((item) => ({
        ...item,
        hazard: "Earthquake",
    }));
    let gt_2 = gt_floods.map((item) => ({
        ...item,
        hazard: "Flood",
    }));
    let gt_3 = gt_cyclones.map((item) => ({
        ...item,
        hazard: "Cyclone",
    }));
    let gt_4 = gt_volcano.map((item) => ({
        ...item,
        hazard: "Eruption",
    }));
    gt_data.push(...gt_1);
    gt_data.push(...gt_2);
    gt_data.push(...gt_3);
    gt_data.push(...gt_4);

    let hn_data = [];
	let hn_1 = hn_earthquakes.map((item) => ({
        ...item,
        hazard: "Earthquake",
    }));
    let hn_2 = hn_floods.map((item) => ({
        ...item,
        hazard: "Flood",
    }));
    let hn_3 = hn_cyclones.map((item) => ({
        ...item,
        hazard: "Cyclone",
    }));
    hn_data.push(...hn_1);
    hn_data.push(...hn_2);
    hn_data.push(...hn_3);

    let elsl_data = [];
	let elsl_1 = elsl_earthquakes.map((item) => ({
        ...item,
        hazard: "Earthquake",
    }));
    let elsl_2 = elsl_floods.map((item) => ({
        ...item,
        hazard: "Flood",
    }));
    let elsl_3 = elsl_cyclones.map((item) => ({
        ...item,
        hazard: "Cyclone",
    }));
    let elsl_4 = elsl_volcano.map((item) => ({
        ...item,
        hazard: "Eruption",
    }));
    elsl_data.push(...elsl_1);
    elsl_data.push(...elsl_2);
    elsl_data.push(...elsl_3);
    elsl_data.push(...elsl_4);

</script>

<div class="flex justify-center items-center">
<ul class="flex">
	<li class="mr-6">
	  <a class="text-blue-500 hover:text-blue-800" href="/" on:click|preventDefault={() => (menu = 1)}>Guatemala</a>
	</li>
	<li class="mr-6">
	  <a class="text-blue-500 hover:text-blue-800" href="/" on:click|preventDefault={() => (menu = 2)}>Honduras</a>
	</li>
	<li class="mr-6">
	  <a class="text-blue-500 hover:text-blue-800" href="/" on:click|preventDefault={() => (menu = 3)}>El Salvador</a>
	</li>
  </ul>
</div>


<section class="graph">
	<h2 style="margin-top: 15px">Timeline of Significant Natural Disasters</h2>

	{#if menu === 1}
    <Testtimeline3 data={gt_data}/>
	<!-- <Testtimeline2 data={gt_data}/> -->
	{:else if menu === 2}
	<Testtimeline3 data={hn_data}/>
	{:else if menu === 3}
	<Testtimeline3 data={elsl_data}/>
	{:else}
	<h1>
		Page Not Found
	</h1>
	{/if}
</section>

<svelte:head>
	<link href="https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css" rel="stylesheet"/>
</svelte:head>

  <style>

	* {
  box-sizing: border-box;
	}

	.graph {
        display: inline-block;
        margin-left: 150px;
    }

	h2 {
        font-size: 15px;
        font-weight: 300;
        line-height: 1.5;
    }


  </style>







