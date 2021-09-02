<script>
	import Header from '$lib/Header.svelte';
	import Directions from '$lib/Directions.svelte';
	import Map from '$lib/Map.svelte';
	import Details from '$lib/Details.svelte';
	import Productive from '$lib/Productive.svelte';
	import Renewables from '$lib/Renewables.svelte';
	import Stats from '$lib/Stats.svelte';
	import Rural from '$lib/Rural.svelte';
	import Shifting from '$lib/Shifting.svelte';
	import ThisIsCosgrove from '$lib/ThisIsCosgrove.svelte';
	import Timeline from '$lib/Timeline.svelte';
</script>

<body>
	<Header />
	<ThisIsCosgrove />
	<Directions />
	<Details />
	<Map />
	<Productive />
	<Stats />
	<Rural />
	<Renewables />
	<Shifting />
	<Timeline />
</body>

<style>
	body {
		margin: 0;
		padding: 0;
	}
</style>
