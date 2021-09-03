<script>
	import { onMount } from 'svelte';

	onMount(async () => {
		let observer = new IntersectionObserver((entries) => {
			entries.forEach((entry) => {
				if (entry.isIntersecting) {
					startAnimation();
				}
			});
		}, {});
		observer.observe(document.querySelector('#melbourne-label'));
	});

	const linePath =
		'M13.7827 402L11.2077 397.371H8.79367L5.7359 398.967L3 396.573V387.794L6.54058 384.761H25.2091V378.057L27.1403 368.161V365.288L23.9216 360.02L17.4842 356.828L15.0702 350.762L17.4842 330.65L22.3122 322.67V318.2L24.4044 313.731L24.8872 307.825L31.3246 300.961L34.7043 297.131V293.3L33.7387 290.107V283.403L36.6355 277.178L40.1761 275.263L41.9464 268.559L41.6245 250.682L45.1651 244.297V235.199L49.6712 220.833L49.9931 211.735L53.3728 206.946L52.4071 194.655L53.3728 187.313L55.7868 184.44L57.5571 177.896L62.3851 176.938V136.714L70.11 126.498V111.015L76.7084 95.692L87.4911 87.5514L90.8707 87.0726L94.5722 83.7206L97.3081 76.5377L104.067 68.876L120 37.91V17';

	let animationStarted = false;
	let interval;
	let animationDuration = 5000; // ms
	let updateSpeed = 50; // ms
	const startAnimation = () => {
		// start after short delay
		setTimeout(() => {
			animationStarted = true;
			interval = setInterval(updateStats, updateSpeed);
		}, 1000);
	};

	let km = 0;
	let destinationKm = 190;
	let hr = 0;
	let min = 0;
	let timeToDestinationInMins = 132;
	let timeInMins = 0;
	const kmIncrement = destinationKm / (animationDuration / updateSpeed);
	const timeIncrement = timeToDestinationInMins / (animationDuration / updateSpeed);
	function updateStats() {
		km = km + kmIncrement;
		timeInMins = timeInMins + timeIncrement;
		hr = Math.floor(timeInMins / 60);
		min = Math.floor(timeInMins % 60);
		if (km >= destinationKm) {
			clearInterval(interval);
			km = destinationKm;
			timeInMins = timeToDestinationInMins;
			hr = Math.floor(timeInMins / 60);
			min = Math.floor(timeInMins % 60);
		}
	}
</script>

<div id="map-directions-container">
	<div class="label shep">Shepparton</div>
	<div id="melbourne-label" class="label melb">Melbourne</div>
	<svg
		id="directions"
		width="131"
		height="418"
		viewBox="0 0 131 418"
		fill="none"
		xmlns="http://www.w3.org/2000/svg"
	>
		<path
			id="directions-path"
			d={linePath}
			class={animationStarted ? 'path-animation' : ''}
			stroke="#3DFA52"
			stroke-width="5"
			stroke-linejoin="bevel"
		/>
		<circle cx="16.0303" cy="407.488" r="7.5" stroke="#3DFA52" stroke-width="5" />
		<circle cx="120.487" cy="10.4454" r="7.5" stroke="#3DFA52" stroke-width="5" />
	</svg>
	<div id="info-container">
		<svg id="north" viewBox="0 0 98 176" fill="none" xmlns="http://www.w3.org/2000/svg">
			<path
				d="M40 141.5H43.115V127.395C43.115 126.8 43.08 125.855 43.045 124.63L42.94 121.165H42.975C43.43 122.075 43.955 123.125 44.585 124.28C45.215 125.435 45.67 126.24 45.985 126.695L55.085 141.5H58.655V117H55.54V131.105C55.54 131.7 55.54 132.68 55.575 134.01C55.61 135.305 55.68 136.425 55.715 137.335H55.68C54.315 134.815 53.475 133.205 52.6 131.805L43.395 117H40V141.5Z"
				fill="white"
			/>
			<path
				d="M97 88C97 112.163 91.5444 133.989 82.7745 149.739C73.9861 165.522 62.0041 175 49 175C35.9959 175 24.0139 165.522 15.2255 149.739C6.4556 133.989 1 112.163 1 88C1 63.8371 6.4556 42.011 15.2255 26.2611C24.0139 10.4777 35.9959 1 49 1C62.0041 1 73.9861 10.4777 82.7745 26.2611C91.5444 42.011 97 63.8371 97 88Z"
				stroke="white"
				stroke-width="2"
			/>
			<path d="M49 87.6666V37.6666" stroke="white" stroke-width="2" stroke-linejoin="bevel" />
			<path
				d="M25.667 57.6667C39.0003 57.6667 49.0003 41 49.0003 34.3334C49.0003 41 59.0003 57.6667 72.3337 57.6667"
				stroke="white"
				stroke-linejoin="bevel"
			/>
		</svg>

		<p>
			If you travel north from Melbourne towards the regional New South Wales border, you’ll reach a
			town called Shepparton.
		</p>
		<div id="stats">
			<div>
				<svg
					width="28"
					height="36"
					viewBox="0 0 28 36"
					fill="none"
					xmlns="http://www.w3.org/2000/svg"
				>
					<path
						d="M14.0007 1.33325C17.4247 1.33876 20.7069 2.70138 23.128 5.12252C25.5492 7.54366 26.9118 10.8259 26.9173 14.2499C26.9173 27.1665 14.0007 34.6664 14.0007 34.6664C14.0007 34.6664 1.08398 27.1665 1.08398 14.2499C1.08949 10.8259 2.45212 7.54366 4.87327 5.12252C7.29442 2.70138 10.5766 1.33876 14.0007 1.33325V1.33325Z"
						stroke="white"
						stroke-width="2"
						stroke-linejoin="bevel"
					/>
					<path
						d="M13.9997 20.9373C17.7851 20.9373 20.8538 17.8686 20.8538 14.0832C20.8538 10.2977 17.7851 7.229 13.9997 7.229C10.2142 7.229 7.14551 10.2977 7.14551 14.0832C7.14551 17.8686 10.2142 20.9373 13.9997 20.9373Z"
						stroke="white"
						stroke-width="2"
						stroke-linejoin="bevel"
					/>
				</svg>
				<div class="stat-text">{km.toFixed(0)}km</div>
			</div>
			<div>
				<svg
					width="36"
					height="36"
					viewBox="0 0 36 36"
					fill="none"
					xmlns="http://www.w3.org/2000/svg"
				>
					<path
						d="M17.9997 34.6666C27.2044 34.6666 34.6663 27.2047 34.6663 17.9999C34.6663 8.79517 27.2044 1.33325 17.9997 1.33325C8.79493 1.33325 1.33301 8.79517 1.33301 17.9999C1.33301 27.2047 8.79493 34.6666 17.9997 34.6666Z"
						stroke="white"
						stroke-width="2"
						stroke-linejoin="bevel"
					/>
					<path
						d="M18 5.5V18L26.3333 26.3333"
						stroke="white"
						stroke-width="2"
						stroke-linejoin="bevel"
					/>
				</svg>
				<div class="stat-text">{hr}hr {min}min</div>
			</div>
		</div>
	</div>
	<img
		id="map-directions"
		src="https://res.cloudinary.com/future-super/image/upload/f_auto,q_auto/v1630563298/melbourne-to-shepparton_2.png"
		alt="Map of Melbourne to Shepparton in Victoria"
	/>
</div>

<style>
	#map-directions-container {
		position: relative;
		width: 100%;
		height: 600px;
		margin-bottom: 100vh;
		display: flex;
		flex-direction: row;
		justify-content: flex-end;
		overflow: hidden;
	}

	#map-directions {
		height: 600px;
	}

	#info-container {
		position: absolute;
		height: 560px;
		width: 40vw;
		top: 20px;
		left: 20px;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-items: flex-start;
		color: var(--white);
	}

	#info-container > p {
		font-size: var(--m);
		margin: 0;
		padding: 0;
	}

	.label {
		font-size: var(--xs);
		color: var(--white);
		position: absolute;
		padding: 10px 20px;
		border: 2px solid var(--white);
		border-radius: 14px;
		text-transform: uppercase;
	}
	.shep {
		top: 74px;
		right: 240px;
	}
	.melb {
		top: 474px;
		right: 86px;
	}

	svg#directions {
		right: 190px;
		top: 50px;
		height: 500px;
		position: absolute;
	}

	path#directions-path {
		fill-opacity: 0;
		stroke-dasharray: 881.51904296875;
		stroke-dashoffset: 881.51904296875;
	}

	svg#north {
		height: 70px;
	}

	svg#north > path {
		stroke-width: 4;
	}

	#stats {
		display: flex;
		flex-direction: row;
	}

	.stat-text {
		font-family: 'MonumentGroteskMono', sans-serif;
		margin-right: 60px;
		font-size: var(--xs);
	}

	.path-animation {
		animation-name: draw;
		animation-duration: 10s; /* double actual time it will take */
		animation-iteration-count: 1;
		animation-timing-function: linear;
		animation-fill-mode: forwards;
	}

	@keyframes draw {
		to {
			stroke-dashoffset: 0;
		}
	}

	@media (max-width: 1000px) {
		.shep {
			top: 80px;
			right: 240px;
		}
		.melb {
			top: 480px;
			right: 120px;
		}
	}

	@media (max-width: 700px) {
		#north {
			margin-top: 16px;
			height: 100;
		}
		svg#north > path {
			stroke-width: 2;
		}
		#map-directions {
			margin-right: -164px;
		}
		svg#directions {
			right: 24px;
		}
		.shep {
			top: 36px;
			right: 20px;
		}
		.melb {
			top: 524px;
			right: 20px;
		}
		#stats {
			flex-direction: column;
		}
		#stats > div > svg > path {
			stroke-width: 1px;
		}
		.stat-text {
			margin-bottom: 13px;
		}
		.label {
			border-width: 1px;
		}
	}
</style>
