<script>
	import mapboxgl from 'mapbox-gl';
	import { onMount } from 'svelte';

	onMount(async () => {
		mapboxgl.accessToken =
			'pk.eyJ1IjoiYW5kcmV3LWZzIiwiYSI6ImNrc2p5cXpjaTJpcTIydHJvODdpMWNhY2sifQ.AMPUDx1H1q5K5bik8ICnvQ';
		const map = new mapboxgl.Map({
			container: 'map', // container ID
			style: 'mapbox://styles/mapbox/satellite-streets-v11', // style URL
			center: [145.5643507, -37.345906], // starting position [lng, lat]
			zoom: 7, // starting zoom
			pitch: 50
		});
		const marker1 = new mapboxgl.Marker().setLngLat([145.5643507, -36.345906]).addTo(map);
	});
</script>

<body>
	<h1>Cosgrove</h1>
	<div id="map" />
</body>

<style>
	body {
		margin: 0;
		padding: 0;
	}
	#map {
		position: absolute;
		top: 0;
		bottom: 0;
		width: 100%;
	}
</style>
