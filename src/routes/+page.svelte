<script lang="ts">
	import { onMount } from 'svelte';
	import mapboxgl from 'mapbox-gl';
	import '../../node_modules/mapbox-gl/dist/mapbox-gl.css';
	import { PUBLIC_MAPBOX_ACCESS_TOKEN, PUBLIC_MAPBOX_STYLE_URL } from '$env/static/public';

	onMount(() => {
		mapboxgl.accessToken = PUBLIC_MAPBOX_ACCESS_TOKEN;

		const map = new mapboxgl.Map({
			container: 'map',
			zoom: 10,
			style: PUBLIC_MAPBOX_STYLE_URL,
			center: [12.92137, 50.827847]
		});
	});
</script>

<h1>Supermarktnavigator</h1>
<div id="map"></div>

<style>
	h1 {
		text-align: center;
	}
	#map {
		position: absolute;
		height: 100%;
		width: 100%;
		padding: 0;
		box-sizing: border-box;
	}
</style>
