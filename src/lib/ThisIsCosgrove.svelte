<div class="container">
	<div class="border">
		<h2>This is<br />Cosgrove<br />Solar</h2>
	</div>
</div>

<style>
	.container {
		height: 86vh;
		background-image: url('https://res.cloudinary.com/future-super/image/upload/f_auto,q_auto/v1630558208/cosgrove-landscape.png');
		background-size: cover;
		background-repeat: no-repeat;
		background-position: top center;
		display: flex;
		justify-content: center;
		align-items: center;
		padding: 20px;
	}
	.border {
		border: var(--border-width) solid var(--black);
		border-radius: var(--border-radius);
		min-width: 60%;
	}
	h2 {
		font-size: var(--l);
		text-transform: uppercase;
		text-align: center;
		padding: 20px;
	}
	@media (max-width: 600px) {
		.border {
			min-width: 100%;
		}
	}
</style>
