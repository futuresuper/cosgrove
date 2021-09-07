<script>
	import { onMount } from 'svelte';

	onMount(async () => {
		let observer = new IntersectionObserver((entries) => {
			entries.forEach((entry) => {
				if (entry.isIntersecting) {
					// console.log(entry.target.id);
					startNumbersTicking(entry.target.id);
				}
			});
		}, {});
		observer.observe(document.querySelector('#mwh'));
		observer.observe(document.querySelector('#homes'));
		observer.observe(document.querySelector('#iphones'));
		observer.observe(document.querySelector('#laptops'));
	});

	const numbersFinal = {
		mwh: 11600,
		homes: 2516,
		iphones: 1076066790,
		laptops: 232000000
	};
	const numbersCurrent = {
		mwh: 0,
		homes: 0,
		iphones: 0,
		laptops: 0
	};
	const animationDuration = {
		mwh: 800,
		homes: 800,
		iphones: 1500,
		laptops: 1100
	};
	const updateSpeed = 50;
	const increments = {
		mwh: numbersFinal.mwh / (animationDuration.mwh / updateSpeed),
		homes: numbersFinal.homes / (animationDuration.homes / updateSpeed),
		iphones: numbersFinal.iphones / (animationDuration.iphones / updateSpeed),
		laptops: numbersFinal.laptops / (animationDuration.laptops / updateSpeed)
	};
	const intervals = {};

	function startNumbersTicking(item) {
		console.log(item + ' | ' + numbersFinal[item]);
		intervals[item] = setInterval(function () {
			numbersCurrent[item] = numbersCurrent[item] + increments[item];
			if (numbersCurrent[item] >= numbersFinal[item]) {
				clearInterval(intervals[item]);
				numbersCurrent[item] = numbersFinal[item];
			}
		}, updateSpeed);
	}

	function updateNumbers(item) {
		console.log(item);
		console.log('numbersCurrent[item]: ' + numbersCurrent[item]);
		console.log('increments[item]: ' + increments[item]);
		numbersCurrent[item] = numbersCurrent[item] + increments[item];
		if (numbersCurrent[item] >= numbersFinal[item]) {
			clearInterval(intervals[item]);
			numbersCurrent[item] = numbersFinal[item];
		}
	}
</script>

<div class="container">
	<p>In a single year Cosgrove will generate:</p>
	<hr />
	<div class="row">
		<div class="left">
			<div class="number">{numbersCurrent.mwh.toFixed(0)}</div>
			<div class="unit">MWH</div>
		</div>
		<svg
			width="134"
			height="134"
			viewBox="0 0 134 134"
			fill="none"
			xmlns="http://www.w3.org/2000/svg"
		>
			<path
				d="M44.6663 111.667L94.9163 55.8335H72.583L89.333 22.3335H55.833L39.083 67.0002H61.4163L44.6663 111.667Z"
				stroke="black"
				stroke-width="5"
				stroke-linejoin="bevel"
			/>
		</svg>
	</div>
	<hr id="mwh" class="last" />
	<p>Which is enough to power the equivalent of:</p>
	<hr />
	<div class="row">
		<div class="left">
			<div class="number">{numbersCurrent.homes.toFixed(0)}</div>
			<div class="unit">Homes</div>
		</div>
		<svg
			width="134"
			height="134"
			viewBox="0 0 134 134"
			fill="none"
			xmlns="http://www.w3.org/2000/svg"
		>
			<path d="M100.5 67V106.083H33.5V67" stroke="black" stroke-width="5" stroke-linejoin="bevel" />
			<path
				d="M22.334 61.4168L67.0005 27.917L111.667 61.4168"
				stroke="black"
				stroke-width="5"
				stroke-linejoin="bevel"
			/>
		</svg>
	</div>
	<hr id="homes" />
	<div class="row">
		<div class="left">
			<div class="number">{numbersCurrent.iphones.toFixed(0)}</div>
			<div class="unit">iPhone 12 Charges</div>
		</div>
		<svg
			width="134"
			height="134"
			viewBox="0 0 134 134"
			fill="none"
			xmlns="http://www.w3.org/2000/svg"
		>
			<path
				d="M89.333 22.3335H44.6663C41.5828 22.3335 39.083 24.8332 39.083 27.9168V106.083C39.083 109.167 41.5828 111.667 44.6663 111.667H89.333C92.4166 111.667 94.9163 109.167 94.9163 106.083V27.9168C94.9163 24.8332 92.4166 22.3335 89.333 22.3335Z"
				stroke="black"
				stroke-width="5"
				stroke-linejoin="bevel"
			/>
			<path
				d="M50.25 22.3335L55.8333 33.5002H78.1667L83.75 22.3335"
				stroke="black"
				stroke-width="5"
				stroke-linejoin="bevel"
			/>
		</svg>
	</div>
	<hr id="iphones" />
	<div class="row">
		<div class="left">
			<div class="number">{numbersCurrent.laptops.toFixed(0)}</div>
			<div class="unit">Laptops</div>
		</div>
		<svg
			width="134"
			height="134"
			viewBox="0 0 134 134"
			fill="none"
			xmlns="http://www.w3.org/2000/svg"
		>
			<path
				d="M106.084 83.75V39.0833C106.084 37.6025 105.495 36.1824 104.448 35.1353C103.401 34.0882 101.981 33.5 100.5 33.5H33.5003C32.0195 33.5 30.5994 34.0882 29.5523 35.1353C28.5052 36.1824 27.917 37.6025 27.917 39.0833V83.75"
				stroke="black"
				stroke-width="5"
				stroke-linejoin="bevel"
			/>
			<path
				d="M111.666 83.75V94.9167C111.666 96.3975 111.078 97.8176 110.031 98.8647C108.984 99.9118 107.564 100.5 106.083 100.5H27.9163C26.4355 100.5 25.0154 99.9118 23.9683 98.8647C22.9213 97.8176 22.333 96.3975 22.333 94.9167V83.75H55.833V89.3333H78.1663V83.75H111.666Z"
				stroke="black"
				stroke-width="5"
				stroke-linejoin="bevel"
			/>
		</svg>
	</div>
	<hr id="laptops" />
</div>

<style>
	.container {
		padding: 20px 20px 20px 20%;
	}

	.row {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
	}

	.left {
		display: flex;
		flex-direction: row;
		align-items: flex-end;
	}

	.number {
		font-family: var(--mono);
		font-size: var(--xxl);
	}

	.unit {
		padding: 4px;
		margin-left: 8px;
		margin-bottom: 20px;
		border: 1px solid var(--black);
		border-radius: 8px;
		font-size: var(--xxs);
		text-transform: uppercase;
	}

	.last {
		margin-bottom: 80px;
	}

	@media (max-width: 800px) {
		.left {
			flex-direction: column;
			align-items: flex-start;
		}
		.container {
			padding: 20px;
		}
		.number {
			font-size: var(--xl);
		}
		.unit {
			margin: 2px 0 0 0;
		}
		svg {
			width: 80px;
		}
	}
</style>
