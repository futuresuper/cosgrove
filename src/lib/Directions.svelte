<script>
	const linePath =
		'M23.7124 766.016L18.7661 757.097H14.129L8.25538 760.172L3 755.559V738.644L9.80108 732.801H45.6613V719.884L49.371 700.816V695.28L43.1882 685.131L30.8226 678.98L26.1855 667.294L30.8226 628.543L40.0968 613.166V604.555L44.1156 595.944L45.043 584.564L57.4086 571.34L63.9005 563.959V556.578L62.0457 550.427V537.51L67.6102 525.516L74.4113 521.825L77.8118 508.909L77.1936 474.464L83.9946 462.162V444.632L92.6505 416.953L93.2688 399.423L99.7608 390.196L97.9059 366.516L99.7608 352.368L104.398 346.833L107.798 334.223L117.073 332.378V254.877L131.911 235.194V205.362L144.586 175.838L165.298 160.153L171.79 159.231L178.901 152.772L184.156 138.933L197.14 124.171L227.745 64.507V24.2188';

	let animationStarted = false;
	const startAnimation = () => {
		console.log('start');
		animationStarted = true;
	};

	// class="path-animation"
</script>

<div id="map-directions-container">
	<button on:click={startAnimation}> START </button>

	<svg
		width="241"
		height="790"
		viewBox="0 0 241 790"
		fill="none"
		xmlns="http://www.w3.org/2000/svg"
	>
		<path
			id="path"
			class={animationStarted ? 'path-animation' : ''}
			d={linePath}
			stroke="#3DFA52"
			stroke-width="5"
			stroke-linejoin="bevel"
		/>
		<circle cx="27" cy="777" r="10.5" stroke="#3DFA52" stroke-width="5" />
		<circle cx="228" cy="13" r="10.5" stroke="#3DFA52" stroke-width="5" />
	</svg>
	<img
		id="map-directions"
		src="https://res.cloudinary.com/future-super/image/upload/v1630460878/map.png"
		alt="Map of Melbourne to Cosgrove in Victoria"
	/>
</div>

<style>
	#map-directions-container {
		position: relative;
		width: 100%;
	}

	#map-directions {
		width: 100%;
	}

	svg {
		right: 7%;
		top: 10%;
		height: 80%;
		position: absolute;
	}

	path {
		fill-opacity: 0;
		stroke-dasharray: 881.51904296875;
		stroke-dashoffset: 881.51904296875;
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
