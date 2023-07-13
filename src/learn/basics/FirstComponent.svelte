<script>
	let name = 'Svelte';
	let string = `this string contains some <strong>HTML!!!</strong>`;
	let clicked = 0;

	$: doubled = clicked * 2;
	$: triple = clicked * 3;

	$: if (clicked > 10) {
		alert("Hello there, you are goind fast huh? Let's reset");
		clicked = 0;
	}

	function increment() {
		clicked += 1;
	}
</script>

<div class="container">
	<h1>Hello World from {name}</h1>
	<p>{@html string}</p>
	<button on:click={increment}>
		This has been clicked {clicked}
		{clicked === 1 ? 'time' : 'times'}
	</button>
	<p>the double for {clicked} is {doubled}</p>
	<p>and the triple is {triple}</p>

	{#if clicked >= 10}
		<p>You are going fast!</p>
	{:else if clicked === 5}
		<p>almost there</p>
	{:else}
		<p>Keep clicking</p>
	{/if}
</div>

<style>
	.container {
		display: flex;
		flex-direction: column;
		height: 100%;
	}

	h1 {
		color: red;
	}

	p {
		font-size: 1rem;
		color: goldenrod;
	}
</style>
