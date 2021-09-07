<script>
	export let label = '';
	export let percent = 0;
</script>

<div>
	<p>{label}</p>
	<div id="outer">
		<div id="inner" style="width:{percent}%" />
	</div>
</div>

<style>
	#outer {
		width: 100%;
		height: 36px;
		background-color: var(--black);
		border-radius: 200px;
	}

	#inner {
		background-color: var(--green);
		border-radius: 200px;
		height: 36px;
	}

	p {
		font-size: var(--xxs);
	}

	@media (max-width: 800px) {
		#outer {
			height: 20px;
		}

		#inner {
			height: 20px;
		}
	}
</style>
