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
    <Testtimeline4 data={gt_data}/>
	{:else if menu === 2}
	<Testtimeline4 data={hn_data}/>
	{:else if menu === 3}
	<Testtimeline4 data={elsl_data}/>
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







