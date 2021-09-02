<script>
	const linePath =
		'M13.7827 402L11.2077 397.371H8.79367L5.7359 398.967L3 396.573V387.794L6.54058 384.761H25.2091V378.057L27.1403 368.161V365.288L23.9216 360.02L17.4842 356.828L15.0702 350.762L17.4842 330.65L22.3122 322.67V318.2L24.4044 313.731L24.8872 307.825L31.3246 300.961L34.7043 297.131V293.3L33.7387 290.107V283.403L36.6355 277.178L40.1761 275.263L41.9464 268.559L41.6245 250.682L45.1651 244.297V235.199L49.6712 220.833L49.9931 211.735L53.3728 206.946L52.4071 194.655L53.3728 187.313L55.7868 184.44L57.5571 177.896L62.3851 176.938V136.714L70.11 126.498V111.015L76.7084 95.692L87.4911 87.5514L90.8707 87.0726L94.5722 83.7206L97.3081 76.5377L104.067 68.876L120 37.91V17';

	// 'M23.7124 766.016L18.7661 757.097H14.129L8.25538 760.172L3 755.559V738.644L9.80108 732.801H45.6613V719.884L49.371 700.816V695.28L43.1882 685.131L30.8226 678.98L26.1855 667.294L30.8226 628.543L40.0968 613.166V604.555L44.1156 595.944L45.043 584.564L57.4086 571.34L63.9005 563.959V556.578L62.0457 550.427V537.51L67.6102 525.516L74.4113 521.825L77.8118 508.909L77.1936 474.464L83.9946 462.162V444.632L92.6505 416.953L93.2688 399.423L99.7608 390.196L97.9059 366.516L99.7608 352.368L104.398 346.833L107.798 334.223L117.073 332.378V254.877L131.911 235.194V205.362L144.586 175.838L165.298 160.153L171.79 159.231L178.901 152.772L184.156 138.933L197.14 124.171L227.745 64.507V24.2188';

	let animationStarted = false;
	const startAnimation = () => {
		console.log('start');
		animationStarted = true;
	};

	// class="path-animation"
</script>

<button on:click={startAnimation}> START </button>
<div id="map-directions-container">
	<div class="label shep">Shepparton</div>
	<div class="label melb">Melbourne</div>
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
				stroke-width="2"
				stroke-linejoin="bevel"
			/>
		</svg>

		<p>
			If you travel north from Melbourne towards the regional New South Wales border, you’ll reach a
			town called Shepparton.
		</p>
		<div id="stats">Stats</div>
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
		right: 110px;
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
		height: 100px;
	}

	.path-animation {
		animation-name: draw;
		animation-duration: 5s;
		animation-iteration-count: 1;
		animation-timing-function: linear;
		animation-fill-mode: forwards;
	}

	@keyframes draw {
		to {
			stroke-dashoffset: 0;
		}
	}
</style>
