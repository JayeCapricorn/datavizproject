<script>
  import { json } from "d3";
  import Marks from "./Marks.svelte";
  let dataset = [];
  json(
    "https://raw.githubusercontent.com/holtzy/D3-graph-gallery/master/DATA/world.geojson"
  ).then((data) => {
    // dataset = data.features;
    dataset = data.features.filter(function(d){ return d.properties.name=="Honduras"});
  });
  const width = 1200,
    height = 600;
</script>

<main>
  <svg {width} {height}>
    <Marks {dataset} />
  </svg>
</main>