<div class="container">
	<div id="first-row">
		<img
			src="https://res.cloudinary.com/future-super/image/upload/f_auto,q_auto/v1630642915/solar-panels-top.png"
			alt="Top view of solar panels"
		/>
		<p id="not-far-from">
			Not far outside the town is a small community made up of farmland, some university campuses, a
			quarry, and what will soon be a revolutionary solar&nbsp;project.
		</p>
	</div>
	<div id="gate-image-container">
		<div id="gate-image"><p>A revolutionary solar&nbsp;project</p></div>
	</div>
	<p id="this-is-the-land">
		This is the land that has been reserved for Cosgrove solar farm. These smaller-scale farms are
		the future, making use of unproductive farmland without the oppressive needs of a large solar
		projects. Yet the impact on locals will&nbsp;be&nbsp;profound.
	</p>
</div>

<style>
	.container {
		padding: 80px 20px;
	}

	#first-row {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
	}

	img {
		width: 44%;
		border-radius: var(--border-radius);
	}

	p#not-far-from {
		width: 44%;
		font-size: var(--s);
	}

	#gate-image-container {
		width: 100%;
		display: flex;
		flex-direction: row;
		justify-content: flex-end;
		margin-top: -50px;
	}

	#gate-image {
		background-image: url('https://res.cloudinary.com/future-super/image/upload/f_auto,q_auto/v1630642915/cosgrove-gate.png');
		background-position: center center;
		background-repeat: no-repeat;
		background-size: cover;
		width: 1045px;
		height: 480px; /* 564px */
		max-width: 70%;
		border-radius: var(--border-radius);
		display: flex;
		justify-content: center;
		align-items: center;
	}

	#gate-image > p {
		font-size: var(--m);
		color: var(--white);
		border: 3px solid var(--white);
		padding: 140px 80px;
		border-radius: 50%;
		text-transform: uppercase;
		text-align: center;
	}

	p#this-is-the-land {
		font-size: var(--l);
		max-width: 70%;
	}

	@media (max-width: 1000px) {
		#gate-image > p {
			max-width: 70%;
			padding: 10% 5%;
		}

		#gate-image-container {
			margin-top: -20px;
		}
	}

	@media (max-width: 700px) {
		img {
			width: 50%;
			height: 300px;
		}

		p#not-far-from {
			width: 44%;
		}

		#gate-image {
			height: 200px;
			max-width: 86%;
		}

		#gate-image > p {
			border-width: 2px;
			padding: 10% 10%;
			border-radius: 50%;
		}
	}

	@media (max-width: 490px) {
		#gate-image {
			max-width: 100%;
		}
	}
</style>
