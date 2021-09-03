<script>
	import { colours } from '$lib/helpers/enums';
	import Logo from './Logo.svelte';
</script>

<header>
	<Logo colour={colours.black} />
	<div class="text">
		<p>We’re changing how you experience your&nbsp;super.</p>
		<p>
			For the first time, you get to follow a solar farm, from the moment you invest, through
			building, to becoming an owner of a renewables producer that powers an entire
			regional&nbsp;community.
		</p>
	</div>

	<svg viewBox="0 0 44 84" fill="none" xmlns="http://www.w3.org/2000/svg">
		<path d="M22 0.125L22 82.0325" stroke="black" stroke-width="6" stroke-linejoin="bevel" />
		<path
			d="M41.542 59.5893L22.0003 82.0343L2.45866 59.5893"
			stroke="black"
			stroke-width="6"
			stroke-linejoin="bevel"
		/>
	</svg>
</header>

<style>
	header {
		padding: 50px;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-items: center;
		min-height: 80vh;
	}
	.text {
		margin: 50px 0;
	}
	p {
		font-size: var(--m);
		text-align: center;
		max-width: 800px;
		margin: 0 0 8px 0;
		padding: 0;
	}
	svg {
		margin-top: -8px;
		height: 70px;
	}
	@media (max-width: 1000px) {
		header {
			padding: 40px;
		}
		svg {
			height: 50px;
		}
	}
	@media (max-width: 600px) {
		header {
			padding: 20px;
			min-height: 70vh;
		}
		.text {
			margin: 30px 0;
		}
		p {
			margin: 0 0 6px 0;
		}
	}
</style>
