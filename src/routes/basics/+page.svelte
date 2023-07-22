<script lang="ts">
	import AwaitBlock from '../../learn/basics/AwaitBlock.svelte';
	import Binding from '../../learn/basics/Binding.svelte';
	import Canvas from '../../learn/basics/Canvas.svelte';
import ColorPicker from '../../learn/basics/ColorPicker.svelte';
	import FirstComponent from '../../learn/basics/FirstComponent.svelte';
	import GroupInputs from '../../learn/basics/GroupInputs.svelte';
	import Mounting from '../../learn/basics/Mounting.svelte';
	import Package from '../../learn/basics/Package.svelte';
	import Reactivity from '../../learn/basics/Reactivity.svelte';
	import TextingArea from '../../learn/basics/TextingArea.svelte';
	import Thing from '../../learn/basics/Thing.svelte';

	const pkg = {
		name: 'svelte',
		speed: 'blazing',
		version: 4,
		website: 'https://svelte.dev'
	};

	let things: { id: number; name: 'apple' | 'banana' | 'carrot' | 'doughnut' | 'egg' }[] = [
		{ id: 1, name: 'apple' },
		{ id: 2, name: 'banana' },
		{ id: 3, name: 'carrot' },
		{ id: 4, name: 'doughnut' },
		{ id: 5, name: 'egg' }
	];
</script>

<svelte:head>
	<title>Basics</title>
	<meta name="description" content="Svelte Basics Learn" />
</svelte:head>

<div>
	<FirstComponent />
	<Reactivity title="Reactivty with props" />
	<Reactivity on:message={(event) => alert(event.detail.text)}/>
	<Package {...pkg} />
	<ColorPicker />
	<AwaitBlock />
	<Canvas />
	<Binding />
	<GroupInputs />
	<TextingArea />

	<Mounting />
	<div class="things">
		<h2>Things</h2>
		{#each things as thing (thing.id)}
			<Thing name={thing.name} />
		{/each}

		<button on:click={() => (things = things.slice(1))}>Remove last thing</button>
	</div>

</div>

<style>
	div {
		flex: 1;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	h2 {
		font-size: 2rem;
		color: black;
		margin: 1rem 0;
	}

	.things {
		margin-top: 1rem;
	}
</style>
