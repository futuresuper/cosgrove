<div class="background">
	<div class="container">
		<div id="circle-container">
			<div id="circle">
				<h2>Shifting the status&nbsp;quo</h2>
			</div>
		</div>

		<div id="text">
			<p>
				It’s not just the type of energy that’s changing. The energy giants (AGL and Origin) are
				controlled by the Minerals Council - Australia’s fossil fuel lobby. By their lead, renewable
				power has been held down, marked up and pushed aside in Australia.
			</p>
			<p>
				Cosgrove is also doing something new. Future Super members financing the project means that
				the ownership is shared by people who will benefit, and we’ve chosen a mid-sized energy
				supplier Mojo. Cheaper energy will flow for the people in this community and fossil fuel
				power will become the ugly duckling of the market. That’s how we plan to put power back in
				the hands of people.
			</p>
		</div>
	</div>
</div>

<style>
	.background {
		background-color: var(--black);
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.container {
		color: white;
		padding: 80px 20px 20px 20px;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		max-width: 900px;
	}

	#circle-container {
		display: flex;
		justify-content: center;
		align-items: flex-start;
		width: 46%;
	}

	#circle {
		width: 24vw;
		height: 24vw;
		border: 4px solid var(--white);
		border-radius: 200px;
		display: flex;
		justify-content: center;
		align-items: center;
		padding: 20px;
	}

	h2 {
		text-align: center;
		text-transform: uppercase;
		font-size: var(--m);
	}

	#text {
		margin-top: 11vw;
		width: 50%;
		font-size: var(--xs);
	}

	@media (max-width: 700px) {
		#circle {
			width: 32vw;
			height: 32vw;
			border-width: 2px;
		}

		h2 {
			font-size: var(--xs);
		}
	}
</style>
