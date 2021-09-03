<script>
	import mapboxgl from 'mapbox-gl';
	import { onMount } from 'svelte';

	onMount(async () => {
		mapboxgl.accessToken =
			'pk.eyJ1IjoiYW5kcmV3LWZzIiwiYSI6ImNrc2p5cXpjaTJpcTIydHJvODdpMWNhY2sifQ.AMPUDx1H1q5K5bik8ICnvQ';

		const map = new mapboxgl.Map({
			container: 'map',
			center: [145.5102271371005, -36.382720302626736], // starting position [lng, lat]
			zoom: 3, // starting zoom
			style: 'mapbox://styles/mapbox/dark-v10',
			antialias: true // create the gl context with MSAA antialiasing, so custom layers are antialiased
		});

		const size = 140;

		// This implements `StyleImageInterface`
		// to draw a pulsing dot icon on the map.
		const pulsingDot = {
			width: size,
			height: size,
			data: new Uint8Array(size * size * 4),

			// When the layer is added to the map,
			// get the rendering context for the map canvas.
			onAdd: function () {
				const canvas = document.createElement('canvas');
				canvas.width = this.width;
				canvas.height = this.height;
				this.context = canvas.getContext('2d');
			},

			// Call once before every frame where the icon will be used.
			render: function () {
				const duration = 1500;
				const t = (performance.now() % duration) / duration;

				const radius = (size / 2) * 0.3;
				const outerRadius = (size / 2) * 0.7 * t + radius;
				const context = this.context;

				// Draw the outer circle.
				context.clearRect(0, 0, this.width, this.height);
				context.beginPath();
				context.arc(this.width / 2, this.height / 2, outerRadius, 0, Math.PI * 2);
				context.fillStyle = `rgba(61, 250, 82, ${1 - t})`;
				context.fill();

				// Draw the inner circle.
				context.beginPath();
				context.arc(this.width / 2, this.height / 2, radius, 0, Math.PI * 2);
				context.fillStyle = 'rgba(61, 250, 82, 1)';
				context.strokeStyle = 'rgba(255,255,255, 0.5)';
				context.lineWidth = 2 + 4 * (1 - t);
				context.fill();
				// context.stroke();

				// Update this image's data with data from the canvas.
				this.data = context.getImageData(0, 0, this.width, this.height).data;

				// Continuously repaint the map, resulting
				// in the smooth animation of the dot.
				map.triggerRepaint();

				// Return `true` to let the map know that the image was updated.
				return true;
			}
		};

		map.on('load', () => {
			map.addImage('pulsing-dot', pulsingDot, { pixelRatio: 2 });

			map.addSource('dot-point', {
				type: 'geojson',
				data: {
					type: 'FeatureCollection',
					features: [
						{
							type: 'Feature',
							geometry: {
								type: 'Point',
								coordinates: [145.63, -36.31] // icon position [lng, lat]
							}
						}
					]
				}
			});
			map.addLayer({
				id: 'layer-with-pulsing-dot',
				type: 'symbol',
				source: 'dot-point',
				layout: {
					'icon-image': 'pulsing-dot'
				}
			});
		});

		// create a custom style layer to implement the WebGL content
		const highlightLayer = {
			id: 'highlight',
			type: 'custom',

			// method called when the layer is added to the map
			// https://docs.mapbox.com/mapbox-gl-js/api/#styleimageinterface#onadd
			onAdd: function (map, gl) {
				// create GLSL source for vertex shader
				const vertexSource = `
uniform mat4 u_matrix;
attribute vec2 a_pos;
void main() {
gl_Position = u_matrix * vec4(a_pos, 0.0, 1.0);
}`;

				// create GLSL source for fragment shader
				const fragmentSource = `
void main() {
gl_FragColor = vec4(0.0, 1.0, 0.0, 0.5);
}`;

				// create a vertex shader
				const vertexShader = gl.createShader(gl.VERTEX_SHADER);
				gl.shaderSource(vertexShader, vertexSource);
				gl.compileShader(vertexShader);

				// create a fragment shader
				const fragmentShader = gl.createShader(gl.FRAGMENT_SHADER);
				gl.shaderSource(fragmentShader, fragmentSource);
				gl.compileShader(fragmentShader);

				// link the two shaders into a WebGL program
				this.program = gl.createProgram();
				gl.attachShader(this.program, vertexShader);
				gl.attachShader(this.program, fragmentShader);
				gl.linkProgram(this.program);

				this.aPos = gl.getAttribLocation(this.program, 'a_pos');

				// define vertices of the triangle to be rendered in the custom style layer
				const topLeft = mapboxgl.MercatorCoordinate.fromLngLat({
					lng: 145.6102271371005, // x
					lat: -36.282720302626736 // y
				});
				const topRight = mapboxgl.MercatorCoordinate.fromLngLat({
					lng: 145.6102271371005,
					lat: -36.33754396413089
				});
				const bottomLeft = mapboxgl.MercatorCoordinate.fromLngLat({
					lng: 145.65390629608015,
					lat: -36.282720302626736
				});
				const bottomRight = mapboxgl.MercatorCoordinate.fromLngLat({
					lng: 145.65390629608015,
					lat: -36.33754396413089
				});

				// create and initialize a WebGLBuffer to store vertex and color data
				this.buffer = gl.createBuffer();
				gl.bindBuffer(gl.ARRAY_BUFFER, this.buffer);
				gl.bufferData(
					gl.ARRAY_BUFFER,
					new Float32Array([
						topLeft.x,
						topLeft.y,
						bottomLeft.x,
						bottomLeft.y,
						topRight.x,
						topRight.y,
						bottomRight.x,
						bottomRight.y
					]),
					gl.STATIC_DRAW
				);
			},

			// method fired on each animation frame
			// https://docs.mapbox.com/mapbox-gl-js/api/#map.event:render
			render: function (gl, matrix) {
				gl.useProgram(this.program);
				gl.uniformMatrix4fv(gl.getUniformLocation(this.program, 'u_matrix'), false, matrix);
				gl.bindBuffer(gl.ARRAY_BUFFER, this.buffer);
				gl.enableVertexAttribArray(this.aPos);
				gl.vertexAttribPointer(this.aPos, 2, gl.FLOAT, false, 0, 0);
				// gl.enable(gl.BLEND);
				// gl.blendFunc(61, 250, 82, 100);
				gl.drawArrays(gl.TRIANGLE_STRIP, 0, 4);
			}
		};

		// add the custom style layer to the map
		map.on('load', () => {
			map.addLayer(highlightLayer, 'building');
		});

		/*
		const map = new mapboxgl.Map({
			container: 'map', // container ID
			style: 'mapbox://styles/mapbox/satellite-streets-v11', // style URL
			center: [145.5643507, -37.345906], // starting position [lng, lat]
			zoom: 7, // starting zoom
			pitch: 50
		});

    */
		// const marker1 = new mapboxgl.Marker().setLngLat([145.5643507, -36.345906]).addTo(map);
	});
</script>

<div id="map-container">
	<div id="map-cropping">
		<p>Drag to move map, Scroll/pinch to zoom</p>
		<div id="map" />
	</div>
</div>

<style>
	#map-container {
		display: flex;
		align-items: center;
		justify-content: center;
		background-color: var(--black);
		padding: 40px 0;
	}

	#map-cropping {
		width: 80%;
		height: 70vh;
		overflow: hidden;
		border-radius: var(--border-radius);
	}

	#map {
		height: 80vh;
	}

	p {
		position: absolute;
		color: var(--white);
		font-size: var(--xs);
		z-index: 99;
		margin: 20px 40px;
		padding: 10px;
		background-color: rgba(0, 0, 0, 0.3);
	}
</style>
