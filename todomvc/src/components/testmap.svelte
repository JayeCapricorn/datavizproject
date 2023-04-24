
  <script>
    import mapboxgl from "mapbox-gl";
    import { onMount } from "svelte";
    export let geoJsonToFit;
  
    mapboxgl.accessToken =
    "pk.eyJ1IjoicGVpcWljIiwiYSI6ImNsZ2JseW13ZDA0ejUzcG85ZmJhN3RndXUifQ.Tbnw2SnV2zigv50y8sZerQ";
  
    let container;
    let map;
  
    let zoomLevel;
  
    function updateZoomLevel() {
      const screenWidth = window.innerWidth;
      zoomLevel = screenWidth <= 600 ? 4 : 5.85; // Adjust these values as needed
    }
  
    function handleResize() {
      updateZoomLevel();
      map.setZoom(zoomLevel);
    }
  
    onMount(() => {
      updateZoomLevel();
      map = new mapboxgl.Map({
        container,
        style: "mapbox://styles/mapbox/light-v11",
        center: [-102.5528, 23.6345],
        zoom: 3,
        attributionControl: true, // removes attribution from the bottom of the map
      });
  
      window.addEventListener("resize", handleResize);
  
      map.on("load", () => {
        map.addSource('lines1', { // usa
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [-95.7129, 37.0902]
                ]
              }
            }
          });
          map.addSource('lines2', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [-95.7129, 37.0902]
                ]
              }
            }
          });
          map.addSource('lines3', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [-95.7129, 37.0902]
                ]
              }
            }
          });
          map.addSource('lines4', { // mexico
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [-102.5528, 23.6345]
                ]
              }
            }
          });
          map.addSource('lines5', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [-102.5528, 23.6345]
                ]
              }
            }
          });
          map.addSource('lines6', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [-102.5528, 23.6345]
                ]
              }
            }
          });
          map.addSource('lines7', { // canada
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [-106.3468, 56.1304]
                ]
              }
            }
          });
          map.addSource('lines8', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [-106.3468, 56.1304]
                ]
              }
            }
          });
          map.addSource('lines9', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [-106.3468, 56.1304]
                ]
              }
            }
          });
          map.addSource('lines10', { // uk
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [-3.4360, 55.3781]
                ]
              }
            }
          });
          map.addSource('lines11', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [-3.4360, 55.3781]
                ]
              }
            }
          });
          map.addSource('lines12', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [-3.4360, 55.3781]
                ]
              }
            }
          });
          map.addSource('lines13', { // germany
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [10.4515, 51.1657]
                ]
              }
            }
          });
          map.addSource('lines14', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [10.4515, 51.1657]
                ]
              }
            }
          });
          map.addSource('lines15', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [10.4515, 51.1657]
                ]
              }
            }
          });
          map.addSource('lines16', { // france
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [2.2137, 46.2276]
                ]
              }
            }
          });
          map.addSource('lines17', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [2.2137, 46.2276]
                ]
              }
            }
          });
          map.addSource('lines18', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [2.2137, 46.2276]
                ]
              }
            }
          });
          map.addSource('lines19', { // spain
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [-3.7492, 40.4637]
                ]
              }
            }
          });
          map.addSource('lines20', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [-3.7492, 40.4637]
                ]
              }
            }
          });
          map.addSource('lines21', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [-3.7492, 40.4637]
                ]
              }
            }
          });
          map.addSource('lines22', { // russia
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [105.3188, 61.5240]
                ]
              }
            }
          });
          map.addSource('lines23', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [105.3188, 61.5240]
                ]
              }
            }
          });
          map.addSource('lines24', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [105.3188, 61.5240]
                ]
              }
            }
          });

          map.addLayer({ // usa
            'id': 'lines1',
            'type': 'line',
            'source': 'lines1',
            'paint': {
              'line-width': 9,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines2',
            'type': 'line',
            'source': 'lines2',
            'paint': {
              'line-width': 9,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines3',
            'type': 'line',
            'source': 'lines3',
            'paint': {
              'line-width': 9,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ // mexico
            'id': 'lines4',
            'type': 'line',
            'source': 'lines4',
            'paint': {
              'line-width': 3,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines5',
            'type': 'line',
            'source': 'lines5',
            'paint': {
              'line-width': 3,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines6',
            'type': 'line',
            'source': 'lines6',
            'paint': {
              'line-width': 3,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ // canada
            'id': 'lines7',
            'type': 'line',
            'source': 'lines7',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines8',
            'type': 'line',
            'source': 'lines8',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines9',
            'type': 'line',
            'source': 'lines9',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ // uk
            'id': 'lines10',
            'type': 'line',
            'source': 'lines10',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines11',
            'type': 'line',
            'source': 'lines11',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines12',
            'type': 'line',
            'source': 'lines12',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ // germany
            'id': 'lines13',
            'type': 'line',
            'source': 'lines13',
            'paint': {
              'line-width': 3,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines14',
            'type': 'line',
            'source': 'lines14',
            'paint': {
              'line-width': 3,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines15',
            'type': 'line',
            'source': 'lines15',
            'paint': {
              'line-width': 3,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ // france
            'id': 'lines16',
            'type': 'line',
            'source': 'lines16',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines17',
            'type': 'line',
            'source': 'lines17',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines18',
            'type': 'line',
            'source': 'lines18',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ // spain
            'id': 'lines19',
            'type': 'line',
            'source': 'lines19',
            'paint': {
              'line-width': 2,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines20',
            'type': 'line',
            'source': 'lines20',
            'paint': {
              'line-width': 2,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines21',
            'type': 'line',
            'source': 'lines21',
            'paint': {
              'line-width': 2,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ // russia
            'id': 'lines22',
            'type': 'line',
            'source': 'lines22',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines23',
            'type': 'line',
            'source': 'lines23',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines24',
            'type': 'line',
            'source': 'lines24',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

        updateBounds();
        map.on("zoom", updateBounds);
        map.on("drag", updateBounds);
        map.on("move", updateBounds);
      });
    });
    
    function updateBounds() {
      const bounds = map.getBounds();
      geoJsonToFit.features[0].geometry.coordinates = [
        bounds._ne.lng,
        bounds._ne.lat,
      ];
      geoJsonToFit.features[1].geometry.coordinates = [
        bounds._sw.lng,
        bounds._sw.lat,
      ];
    }
  
  </script>
  
  <svelte:head>
    <link
      rel="stylesheet"
      href="https://api.mapbox.com/mapbox-gl-js/v2.14.0/mapbox-gl.css"
    />
  </svelte:head>
  
  <div class="map" bind:this={container} />
  
  <style>
    .map {
      width: 90%;
      height: 90%; /* check problem when setting width */
      position: absolute;
      transition: opacity 2s, visibility 2s;
      /* outline: blue solid 3px; */
    }
  
  </style>
  
  