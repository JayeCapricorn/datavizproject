<script>
  import Testtimeline4 from "./testtimeline4.svelte";
  import item from "../data/timelinedata3.json";

	export let menu = 4;

  let gt_data = item.filter(function (entry) {
    return entry.Country === "Guatemala";
  });

  let hn_data = item.filter(function (entry) {
    return entry.Country === "Honduras";
  });

  let elsl_data = item.filter(function (entry) {
    return entry.Country === "El Salvador";
  });
</script>

<!-- <div class="flex justify-center items-center">
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
</div> -->

<section class="graph">
  <h2 style="margin-top: 10px;">
    Natural Hazards Timeline
  </h2>
  <div class="dropdownmenu">
    <label for="countries">Choose country:</label>

  <select name="countries" bind:value={menu}>
    <option value={4}>All</option>
    <option value={1}>Guatemala</option>
    <option value={2}>Honduras</option>
    <option value={3}>El Salvador</option>
  </select>
  </div>
  <h3>
    In 2017, Guatemala ranked fourth in the world for risk of being seriously
    impacted by a natural disaster. Residents of El Salvador are also no
    strangers to hurricanes, tropical storms, and earthquakes-
    <br /> 88% of El Salvador is at risk of severe impact from natural
    disasters, with 95% of El Salvador's population at some risk of being
    affected by these damaging weather events. Due to a large majority of
    <br /> the country being impoverished, in 2021, the Inter-American Development
    Bank approved a continent loan of $400 million to aid the country in dealing
    with the effects of natural disasters.
  </h3>

	{#if menu === 4}
    <Testtimeline4 data={item} menu={menu}/>
  {:else if menu === 1}
  <Testtimeline4 data={gt_data} menu={menu}/>
	{:else if menu === 2}
	<Testtimeline4 data={hn_data} menu={menu}/>
	{:else if menu === 3}
	<Testtimeline4 data={elsl_data} menu={menu}/>
	{:else}
	<h1>
		Page Not Found
	</h1>
	{/if}
</section>

<!-- <svelte:head>
	<link href="https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css" rel="stylesheet"/>
</svelte:head> -->

<style>
  @import url("https://fonts.googleapis.com/css2?family=Nunito:wght@300;400;700&display=swap");
  /* :root {
        --color-bg: #ffffff;
        --color-outline: #c2c2c2;
        --color-shadow: hsl(0, 0%, 0%, 0.1);
        --color-text: #3f4252;
        --color-bg-1: hsla(0, 0%, 0%, 0.2);
        --color-shadow-1: hsl(0, 0%, 96%);
    } */
  /* *,
    *::before,
    *::after {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    } */

  select {
    font-family: "Nunito", sans-serif;
  }

  .dropdownmenu {
    font-family: "Nunito", sans-serif;
    /* position: relative;
  top: 90px; */
    /* margin-left: 900px; */
    /* text-align: center; */
  }

  * {
    box-sizing: border-box;
  }

  .graph {
    margin: auto;
    text-align: center;
  }

  h2 {
    /* position: relative;
    top: 80px; */
    font-size: 20px;
    font-weight: 300;
    line-height: 1.5;
    font-family: "Nunito", sans-serif;
  }

  h3 {
    /* position: relative;
      top: 80px; */
    font-size: 10px;
    font-family: "Nunito", sans-serif;
  }

  /* li {
    	display: inline;
  	} */
</style>
