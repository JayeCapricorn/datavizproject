<script>
	import Timeline from "./Timeline.svelte";
	import { testdates, testdates2, testdates3 } from "../data/timelinedata";
	import Testtimeline from '../components/testtimeline.svelte';
	import { gt_earthquakes, hn_earthquakes, elsl_earthquakes, gt_floods, hn_floods, elsl_floods,
	         gt_cyclones, hn_cyclones, elsl_cyclones, gt_volcano, elsl_volcano } from "../data/timelinedata2";

	export let menu = 1;

</script>

<!-- <header>
<ul id="menu">
	<li><a href="/" on:click|preventDefault={() => (menu = 1)}>Guatemala</a></li> |
	<li><a href="/" on:click|preventDefault={() => (menu = 2)}>Honduras</a></li> |
	<li><a href="/" on:click|preventDefault={() => (menu = 3)}>El Salvador</a></li>
</ul>
</header> -->

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
	<h2 style="margin-top: 15px">Earthquakes</h2>

	{#if menu === 1}
	<Testtimeline data={gt_earthquakes} eventname="earthquake"/>
	{:else if menu === 2}
	<Testtimeline data={hn_earthquakes} eventname="earthquake"/>
	{:else if menu === 3}
	<Testtimeline data={elsl_earthquakes} eventname="earthquake"/>
	{:else}
	<h1>
		Page Not Found
	</h1>
	{/if}
</section>

<section class="graph">
	<h2 style="margin-top: 15px">Floods</h2>

	{#if menu === 1}
	<Testtimeline data={gt_floods} eventname="flood"/>
	{:else if menu === 2}
	<Testtimeline data={hn_floods} eventname="flood"/>
	{:else if menu === 3}
	<Testtimeline data={elsl_floods} eventname="flood"/>
	{:else}
	<h1>
		Page Not Found
	</h1>
	{/if}
</section>

<section class="graph">
	<h2 style="margin-top: 15px">Tropical Cyclones</h2>

	{#if menu === 1}
	<Testtimeline data={gt_cyclones} eventname="cyclone"/>
	{:else if menu === 2}
	<Testtimeline data={hn_cyclones} eventname="cyclone"/>
	{:else if menu === 3}
	<Testtimeline data={elsl_cyclones} eventname="cyclone"/>
	{:else}
	<h1>
		Page Not Found
	</h1>
	{/if}
</section>

<section class="graph">
	{#if menu === 1}
	<h2 style="margin-top: 15px">Volcanic Eruptions</h2>
	<Testtimeline data={gt_volcano} eventname="eruption"/>
	{:else if menu === 3}
	<h2 style="margin-top: 15px">Volcanic Eruptions</h2>
	<Testtimeline data={elsl_volcano} eventname="eruption"/>
	{:else}
	<h1>
	</h1>
	{/if}
</section>

<!-- <main>
<div class="timeline">
	{#each  testdates  as {name, date}, i}
		<Event 
		{date} 
		{name}
		isLeft = {i%2 === 0}
		eventID={name}/>
	{/each}
  </div>
</main> -->

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

	/* header {
		position: fixed;
		top: 0;
		background: #f99e58;
		width: 100%;
		height: 100px;
		padding: 5px;
		z-index: 10;
	} */


  </style>







