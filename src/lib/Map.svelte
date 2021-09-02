<script>
	import mapboxgl from 'mapbox-gl';
	import { onMount } from 'svelte';

	onMount(async () => {
		mapboxgl.accessToken =
			'pk.eyJ1IjoiYW5kcmV3LWZzIiwiYSI6ImNrc2p5cXpjaTJpcTIydHJvODdpMWNhY2sifQ.AMPUDx1H1q5K5bik8ICnvQ';

		const map = new mapboxgl.Map({
			container: 'map',
			center: [145.24138875562613, -36.59965724996925], // starting position [lng, lat]
			zoom: 9, // starting zoom
			style: 'mapbox://styles/mapbox/dark-v10',
			antialias: true // create the gl context with MSAA antialiasing, so custom layers are antialiased
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
		const marker1 = new mapboxgl.Marker().setLngLat([145.5643507, -36.345906]).addTo(map);
    */
	});
</script>

<div id="map" />

<style>
	#map {
		width: 100%;
		height: 70vh;
	}
</style>
