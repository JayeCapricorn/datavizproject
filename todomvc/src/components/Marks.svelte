<script>
  import * as d3 from 'd3';
    import { geoPath, geoNaturalEarth1 } from "d3";
    export let dataset = [];
    import { draw } from "svelte/transition";
    import { quadInOut } from "svelte/easing";
    const projection = geoNaturalEarth1().scale(300);
    // let projection = d3.geoTransverseMercator()
    // .rotate([74 + 30 / 60, -38 - 50 / 60])
    // .fitExtent([[20, 20], [940, 480]], dataset);
    const width = 1200,
    height = 600;
    // const projection = d3.geoOrthographic()
    //   .scale(300)
    //   .translate([width / 2, height / 2]);
    const path = geoPath().projection(projection); //(projection);
  </script>
  
{#each  dataset  as data}
  <path  d={path(data)} />
{/each}
  
  <style>
    path {
      fill: none;
      stroke: darkgreen;
    }
  </style>