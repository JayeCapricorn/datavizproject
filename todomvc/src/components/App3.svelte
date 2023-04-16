<script>
    import Testtimeline4 from './testtimeline4.svelte';
	import item from '../data/timelinedata3.json';

	export let menu = 1;
    
    let gt_data = item.filter(function (entry) {
        return entry.Country === 'Guatemala';
    });

    let hn_data = item.filter(function (entry) {
        return entry.Country === 'Honduras';
    });

    let elsl_data = item.filter(function (entry) {
        return entry.Country === 'El Salvador';
    });

</script>

<div class="dropdownmenu">
<label for="countries">Choose country:</label>

<select name="countries" bind:value={menu}>
	<option value={1}>Guatemala</option>
	<option value={2}>Honduras</option>
	<option value={3}>El Salvador</option>
</select>
</div>

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
	<h2 style="margin-top: 15px">Timeline of Significant Natural Disasters</h2>

	{#if menu === 1}
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
	text-align: center;
   }

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
		font-family: "Nunito", sans-serif;
    }

	/* li {
    	display: inline;
  	} */


  </style>







