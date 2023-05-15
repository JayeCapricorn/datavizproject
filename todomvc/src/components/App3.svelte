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
  <h2>
    Natural Hazards in Central America
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
    <b>Natural Hazard:</b> Environmental phenomena potiantially impactful on human societies and environment.
    <br /> <br /> Natural disasters do not occur monolithically; they often cause secondary hazard events and thus form a chain reaction.
    These life-threatening and property-damaging events have been frequently happening in Central America.
    A significant number of casualities and economic loss are reported in these regions every year.
    This timelines illustrates the hazards that happened from 1960 to 2022 chronologically compound with the number of people affected and economic damage.
    The curve of each disaster indicates its frequency.
    <br />
    <br /> <b>Guatemala:</b> Flooding, earthquakes, landslides, tsunamis are most common hazards in Guatemala.
    In 2017, Guatemala ranked <strong style='color:brown;font-size:18px'>Fourth </strong>in the world for risk of being seriously
    impacted by a natural disaster.
    <br /> <b>Honduras:</b> Earthquakes, floods, hurricanes, and droughts affect the people of Honduras.
    Due to a large majority of the country being impoverished.
    In 2021, the Inter-American Development Bank approved a continent loan of $400 million to aid the country in dealing with the effects of natural disasters.
    <br /> <b>El Salvador:</b>
    Residents of El Salvador are no strangers to hurricanes, tropical storms, and earthquakes—
    88% of El Salvador is at risk of severe impact from natural disasters,
    with <strong style='color:brown;font-size:18px'>95%</strong> of El Salvador’s population at some risk of being affected by these damaging weather events.
    <!-- Although the financial impact of natural hazards are widely valued, the human movement associated with these hazards and compound events are easily underestimated. -->
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

  <h2 class="question">
    How do these frequent natural hazards affect migration?
  </h2>
</section>

<!-- <svelte:head>
	<link href="https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css" rel="stylesheet"/>
</svelte:head> -->

<style>
  @import url("https://fonts.googleapis.com/css2?family=Nunito:wght@300;400;700&display=swap");
  @import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@300&display=swap");
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
    font-size: 40px;
    padding:110px 0 20px 0;
    margin:0;
    margin-top: -70px;
    /* font-weight: 300; */
    line-height: 1.5;
    font-family: "Nunito", sans-serif;
  }

  h3 {
    /* position: relative;
      top: 80px; */
    font-weight:400;
    font-size: 18px;
    font-family: 'Open Sans', sans-serif;
    text-align: justify;
    padding:10px 120px ;
  }

  section{
    background-color: #ffffff;
  }

  :global(body) {
    margin: 0;
    background-color: #efe9dd;
  }

  .question {
    padding-top: 40vh;
    padding-bottom: 50vh;
  }

  /* li {
    	display: inline;
  	} */
</style>
