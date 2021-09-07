<div id="container">
	<div id="border">
		<h2>100%&nbsp;Renewables</h2>
	</div>
</div>

<style>
	#container {
		background-image: url('https://res.cloudinary.com/future-super/image/upload/f_auto,q_auto/v1630642915/panels2.png');
		background-position: center center;
		background-repeat: no-repeat;
		background-size: cover;
		border-radius: var(--border-radius);
		display: flex;
		justify-content: center;
		align-items: center;
		margin: 20px;
		height: 90vh;
	}
	#border {
		display: flex;
		justify-content: center;
		align-items: center;
		width: 80%;
		height: 80%;
		border: 4px solid var(--white);
		border-radius: 75% 25%;
	}
	h2 {
		font-size: var(--l);
		color: var(--white);
		text-transform: uppercase;
		text-align: center;
	}

	@media (max-width: 700px) {
		div {
			height: 60vh;
		}
	}

	@media (max-width: 490px) {
		h2 {
			border-radius: var(--border-radius);
		}
	}
</style>
