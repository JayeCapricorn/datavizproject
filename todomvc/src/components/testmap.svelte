
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
          map.addSource('lines25', { // nicaragua
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [-85.2072, 12.8654]
                ]
              }
            }
          });
          map.addSource('lines26', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [-85.2072, 12.8654]
                ]
              }
            }
          });
          map.addSource('lines27', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [-85.2072, 12.8654]
                ]
              }
            }
          });
          map.addSource('lines28', { // costa rica
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [-83.7534, 9.7489]
                ]
              }
            }
          });
          map.addSource('lines29', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [-83.7534, 9.7489]
                ]
              }
            }
          });
          map.addSource('lines30', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [-83.7534, 9.7489]
                ]
              }
            }
          });
          map.addSource('lines31', { // panama
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [-80.7821, 8.5380]
                ]
              }
            }
          });
          map.addSource('lines32', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [-80.7821, 8.5380]
                ]
              }
            }
          });
          map.addSource('lines33', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [-80.7821, 8.5380]
                ]
              }
            }
          });
          map.addSource('lines34', { // venezuela
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [-66.5897, 6.4238]
                ]
              }
            }
          });
          map.addSource('lines35', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [-66.5897, 6.4238]
                ]
              }
            }
          });
          map.addSource('lines36', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [-66.5897, 6.4238]
                ]
              }
            }
          });
          map.addSource('lines37', { // colombia
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [-74.2973, 4.5709]
                ]
              }
            }
          });
          map.addSource('lines38', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [-74.2973, 4.5709]
                ]
              }
            }
          });
          map.addSource('lines39', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [-74.2973, 4.5709]
                ]
              }
            }
          });
          map.addSource('lines40', { // ecuador
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [-78.1834, -1.8312]
                ]
              }
            }
          });
          map.addSource('lines41', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [-78.1834, -1.8312]
                ]
              }
            }
          });
          map.addSource('lines42', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [-78.1834, -1.8312]
                ]
              }
            }
          });
          map.addSource('lines43', { // brazil
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [-51.9253, -14.2350]
                ]
              }
            }
          });
          map.addSource('lines44', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [-51.9253, -14.2350]
                ]
              }
            }
          });
          map.addSource('lines45', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [-51.9253, -14.2350]
                ]
              }
            }
          });
          map.addSource('lines46', { // bolivia
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [-63.5887, -16.2902]
                ]
              }
            }
          });
          map.addSource('lines47', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [-63.5887, -16.2902]
                ]
              }
            }
          });
          map.addSource('lines48', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [-63.5887, -16.2902]
                ]
              }
            }
          });
          map.addSource('lines49', { // australia
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [133.7751, -25.2744]
                ]
              }
            }
          });
          map.addSource('lines50', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [133.7751, -25.2744]
                ]
              }
            }
          });
          map.addSource('lines51', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [133.7751, -25.2744]
                ]
              }
            }
          });
          map.addSource('lines52', { // portugal
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [-8.2245, 39.3999]
                ]
              }
            }
          });
          map.addSource('lines53', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [-8.2245, 39.3999]
                ]
              }
            }
          });
          map.addSource('lines54', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [-8.2245, 39.3999]
                ]
              }
            }
          });
          map.addSource('lines55', { // finland
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [25.7482, 61.9241]
                ]
              }
            }
          });
          map.addSource('lines56', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [25.7482, 61.9241]
                ]
              }
            }
          });
          map.addSource('lines57', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [25.7482, 61.9241]
                ]
              }
            }
          });
          map.addSource('lines58', { // sweden
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [18.6435, 60.1282]
                ]
              }
            }
          });
          map.addSource('lines59', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [18.6435, 60.1282]
                ]
              }
            }
          });
          map.addSource('lines60', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [18.6435, 60.1282]
                ]
              }
            }
          });
          map.addSource('lines61', { // belgium
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [4.4699, 50.5039]
                ]
              }
            }
          });
          map.addSource('lines62', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [4.4699, 50.5039]
                ]
              }
            }
          });
          map.addSource('lines63', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [4.4699, 50.5039]
                ]
              }
            }
          });
          map.addSource('lines64', { // italy
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [12.5674, 41.8719]
                ]
              }
            }
          });
          map.addSource('lines65', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [12.5674, 41.8719]
                ]
              }
            }
          });
          map.addSource('lines66', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [12.5674, 41.8719]
                ]
              }
            }
          });
          map.addSource('lines67', { // poland
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-86.2419, 15.2000],
                  [19.1451, 51.9194]
                ]
              }
            }
          });
          map.addSource('lines68', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-88.8965, 13.7942],
                  [19.1451, 51.9194]
                ]
              }
            }
          });
          map.addSource('lines69', {
          'type': 'geojson',
          'data': {
            'type': 'Feature',
            'properties': {},
            'geometry': {
                'type': 'LineString',
                'coordinates': [
                  [-90.2308, 15.7835],
                  [19.1451, 51.9194]
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

          map.addLayer({ // nicaragua
            'id': 'lines25',
            'type': 'line',
            'source': 'lines25',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines26',
            'type': 'line',
            'source': 'lines26',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines27',
            'type': 'line',
            'source': 'lines27',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ // costa rica
            'id': 'lines28',
            'type': 'line',
            'source': 'lines28',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines29',
            'type': 'line',
            'source': 'lines29',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines30',
            'type': 'line',
            'source': 'lines30',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ 
            'id': 'lines31',
            'type': 'line',
            'source': 'lines31',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines32',
            'type': 'line',
            'source': 'lines32',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines33',
            'type': 'line',
            'source': 'lines33',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ 
            'id': 'lines34',
            'type': 'line',
            'source': 'lines34',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines35',
            'type': 'line',
            'source': 'lines35',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines36',
            'type': 'line',
            'source': 'lines36',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ 
            'id': 'lines37',
            'type': 'line',
            'source': 'lines37',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines38',
            'type': 'line',
            'source': 'lines38',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines39',
            'type': 'line',
            'source': 'lines39',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ 
            'id': 'lines40',
            'type': 'line',
            'source': 'lines40',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines41',
            'type': 'line',
            'source': 'lines41',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines42',
            'type': 'line',
            'source': 'lines42',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ 
            'id': 'lines43',
            'type': 'line',
            'source': 'lines43',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines44',
            'type': 'line',
            'source': 'lines44',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines45',
            'type': 'line',
            'source': 'lines45',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ 
            'id': 'lines46',
            'type': 'line',
            'source': 'lines46',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines47',
            'type': 'line',
            'source': 'lines47',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines48',
            'type': 'line',
            'source': 'lines48',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ 
            'id': 'lines49',
            'type': 'line',
            'source': 'lines49',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines50',
            'type': 'line',
            'source': 'lines50',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines51',
            'type': 'line',
            'source': 'lines51',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ 
            'id': 'lines52',
            'type': 'line',
            'source': 'lines52',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines53',
            'type': 'line',
            'source': 'lines53',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines54',
            'type': 'line',
            'source': 'lines54',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ 
            'id': 'lines55',
            'type': 'line',
            'source': 'lines55',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines56',
            'type': 'line',
            'source': 'lines56',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines57',
            'type': 'line',
            'source': 'lines57',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ 
            'id': 'lines58',
            'type': 'line',
            'source': 'lines58',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines59',
            'type': 'line',
            'source': 'lines59',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines60',
            'type': 'line',
            'source': 'lines60',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ 
            'id': 'lines61',
            'type': 'line',
            'source': 'lines61',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines62',
            'type': 'line',
            'source': 'lines62',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines63',
            'type': 'line',
            'source': 'lines63',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ 
            'id': 'lines64',
            'type': 'line',
            'source': 'lines64',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines65',
            'type': 'line',
            'source': 'lines65',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines66',
            'type': 'line',
            'source': 'lines66',
            'paint': {
              'line-width': 1,
              'line-color': '#3bb2d0' // guatemala
            }
          });

          map.addLayer({ 
            'id': 'lines67',
            'type': 'line',
            'source': 'lines67',
            'paint': {
              'line-width': 1,
              'line-color': '#e55e5e' // honduras
            }
          });

          map.addLayer({
            'id': 'lines68',
            'type': 'line',
            'source': 'lines68',
            'paint': {
              'line-width': 1,
              'line-color': '#fbb03b' // el salvador
            }
          });

          map.addLayer({
            'id': 'lines69',
            'type': 'line',
            'source': 'lines69',
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
  
  