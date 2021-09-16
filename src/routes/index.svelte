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
	import Footer from '$lib/Footer.svelte';

	import { onMount } from 'svelte';
	let password = '';
	let passwordCorrectOrNotNeeded = false;
	let showFailure = false;
	onMount(async () => {
		console.log('HOST: ' + window.location.hostname);
		if (!window.location.hostname.includes('cosgrove.futuresuper')) {
			passwordCorrectOrNotNeeded = true;
		}
	});
</script>

<body>
	{#if passwordCorrectOrNotNeeded}
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
		<Footer />
	{:else}
		<!-- else content here -->
		<div class="password">
			<h2>Password</h2>
			<div>
				<input bind:value={password} />
				<button
					on:click={() =>
						password === 'F0$$ilFr33' ? (passwordCorrectOrNotNeeded = true) : (showFailure = true)}
					>GO</button
				>
			</div>

			{#if showFailure}
				<p>Nope!</p>
			{/if}
		</div>
	{/if}
</body>

<style>
	body {
		margin: 0;
		padding: 0;
	}
	.password {
		height: 100vh;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 80px;
	}
</style>
