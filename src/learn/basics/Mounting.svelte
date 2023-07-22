<script lang="ts">
	import { onMount } from 'svelte';

	function paint(context: CanvasRenderingContext2D, t: number) {
		const { width, height } = context.canvas;
		const imageData = context.getImageData(0, 0, width, height);

		for (let p = 0; p < imageData.data.length; p += 4) {
			const i = p / 4;
			const x = i % width;
			const y = (i / width) >>> 0;

			const red = 64 + (128 * x) / width + 64 * Math.sin(t / 1000);
			const green = 64 + (128 * y) / height + 64 * Math.cos(t / 1000);
			const blue = 128;

			imageData.data[p + 0] = red;
			imageData.data[p + 1] = green;
			imageData.data[p + 2] = blue;
			imageData.data[p + 3] = 255;
		}

		context.putImageData(imageData, 0, 0);
	}

	onMount(() => {
		const canvas = document.querySelector('#gradient')! as HTMLCanvasElement
		const context = canvas.getContext('2d')!

		let frame = requestAnimationFrame(function loop(t) {
			frame = requestAnimationFrame(loop);
			paint(context, t);
		});

		return () => {
			cancelAnimationFrame(frame);
		};
	});
</script>

<canvas id="gradient" width="32" height="32" />

<style>
	canvas {
		position: fixed;
		left: 2rem;
		bottom: 2rem;
		width: 100px;
		height: 100px;
		background-color: #666;
		mask: url($lib/images/gradient.svg) 50% 50% no-repeat;
		mask-size: 64px;
		-webkit-mask: url($lib/images/gradient.svg) 50% 50% no-repeat;
		-webkit-mask-size: 64px;
	}
</style>
