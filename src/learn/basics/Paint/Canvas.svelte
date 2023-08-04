<script lang="ts">
	import { onMount } from 'svelte';

	type Point = { x: number; y: number };

	export let color: string;
	export let size: number;
	export let shouldDraw: boolean = false;

	let canvas: HTMLCanvasElement;
	let context: CanvasRenderingContext2D;
	let previous: Point | null;

	function get_coords(e: MouseEvent) {
		const { clientX, clientY } = e;
		const { left, top } = canvas.getBoundingClientRect();
		const x = clientX - left;
		const y = clientY - top;

		return { x, y };
	}

	function onPointerDown(
		e: PointerEvent & {
			currentTarget: EventTarget & HTMLCanvasElement;
		}
	) {
		if (shouldDraw) {
			const coords = get_coords(e);
			context.fillStyle = color;
			context.beginPath();
			context.arc(coords.x + 300, coords.y + 100, size / 2, 0, 2 * Math.PI);
			context.fill();
			previous = coords;
		}
	}

	function onPointerMove(
		e: PointerEvent & {
			currentTarget: EventTarget & HTMLCanvasElement;
		}
	) {
		const coords = get_coords(e);

		if (e.buttons === 1 && previous && shouldDraw) {
			e.preventDefault();

			context.strokeStyle = color;
			context.lineWidth = size;
			context.lineCap = 'round';
			context.beginPath();
			context.moveTo(previous.x + 300 , previous.y + 100);
			context.lineTo(coords.x + 300, coords.y + 100);
			context.stroke();
		}

		previous = coords;
	}

	function onPointerOut() {
		previous = null;
	}

	onMount(() => {
		context = canvas.getContext('2d')!;

		function resize() {
			canvas.width = window.innerWidth;
			canvas.height = window.innerHeight;
		}

		window.addEventListener('resize', resize);
		resize();

		return () => {
			window.removeEventListener('resize', resize);
		};
	});
</script>

<canvas
	bind:this={canvas}
	on:pointerdown={onPointerDown}
	on:pointerleave={onPointerOut}
	on:pointermove={onPointerMove}
/>

{#if previous}
	<div
		class="preview"
		style="--color: {color}; --size: {size}px; --x: {previous.x}px; --y: {previous.y}px"
	/>
{/if}

<style>
	canvas {
		position: relative;
		width: 400px;
		height: 400px;
	}

	.preview {
		position: absolute;
		left: var(--x);
		top: var(--y);
		width: var(--size);
		height: var(--size);
		transform: translate(-50%, -50%);
		background: var(--color);
		border-radius: 50%;
		opacity: 0.5;
		pointer-events: none;
	}
</style>
