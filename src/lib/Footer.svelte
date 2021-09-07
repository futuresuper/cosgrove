<script>
	import Logo from './Logo.svelte';
</script>

<footer>
	<div class="container">
		<div class="logo-container">
			<Logo colour="white" />
		</div>
		<div>
			<p>
				We acknowledge the Traditional Custodians of the lands on which we operate. We pay our
				respects to their Elders, past, present and emerging, and recognise that sovereignty was
				never ceded. See our <a
					href="https://www.futuresuper.com.au/rap"
					style="color: black; text-decoration: underline;">Reconciliation Action Plan.</a
				>
			</p>
			<p>
				All information provided is general in nature only. We recommend you seek financial advice
				when considering if Future Super is right for your objectives and needs. When considering
				returns, past performance is not indicative of future performance.
			</p>
			<p class="footer-links">
				<a href="https://www.futuresuper.com.au/fund-information/">Fund Information</a>
				<span> • </span>
				<a href="https://www.futuresuper.com.au/terms-and-conditions/">Terms & Conditions</a>
				<span> • </span>
				<a href="https://www.futuresuper.com.au/privacy-policy/">Privacy Policy</a>
			</p>
		</div>
	</div>
</footer>

<style>
	footer {
		padding: 20px;
		font-family: var(--mono);
	}

	.container {
		background-color: #fbf9f9;
		padding: 40px;
		border-radius: var(--border-radius);
		display: flex;
		flex-direction: row;
	}

	.logo-container {
		margin-right: 40px;
		background-color: var(--black);
		padding: 10px;
		height: 130px;
		width: 132px;
		border-radius: 50%;
	}

	p {
		margin-top: 0;
		font-size: var(--xs);
	}

	.footer-links > a {
		font-size: var(--xs);
		color: var(--black);
	}

	@media (max-width: 1000px) {
		.footer-links > a {
			display: block;
			margin-bottom: 6px;
		}

		.container {
			padding: 40px 20px;
		}

		.logo-container {
			margin-right: 20px;
			height: 91px;
			width: 92px;
		}

		.footer-links > span {
			display: none;
		}
	}
</style>
