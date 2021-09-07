<script>
	import Progress from './Progress.svelte';
</script>

<div class="container">
	<p>
		As so often is the case, good things take time. Cosgrove is on track to be up and operational in
		the near future. Keep an eye on your email and this page for future updates.
	</p>
	<h3>Current project timeline</h3>
	<div id="timelines">
		<Progress label="Planning" percent="100" />
		<Progress label="Approval" percent="80" />
		<Progress label="Construction" percent="0" />
	</div>
</div>

<style>
	.container {
		padding: 20px;
	}

	#timelines {
		display: grid;
		grid-template-columns: 1fr 1fr 1fr;
		column-gap: 40px;
		margin-bottom: 80px;
	}

	p {
		font-size: var(--m);
		max-width: 70%;
		margin-bottom: 60px;
	}

	h3 {
		font-size: var(--xs);
		font-weight: 400;
	}

	@media (max-width: 800px) {
		#timelines {
			column-gap: 20px;
		}
	}
</style>
