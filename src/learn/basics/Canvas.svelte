<script lang="ts">
    import { createEventDispatcher } from "svelte"

	let m = { x: 0, y: 0 };
    const dispatch = createEventDispatcher()

	function handleMove(event: MouseEvent) {
		m.x = event.clientX;
		m.y = event.clientY;
	}

    function sayHello() {
        dispatch("message", {
            text: "Hello"
        })
    }
</script>

<div class="container">
	<p>The pointer position is {m.x} and {m.y}</p>
	<button on:click|once={() => alert(`${m.x} and ${m.y}`)}>
		Alert one time the mouse position
	</button>
	<canvas on:mousemove={handleMove} on:click={sayHello} class="root" width="100" height="100" />
</div>

<style>
	.container {
		margin-top: 2rem;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	canvas {
		border: 1px solid black;
	}
</style>
