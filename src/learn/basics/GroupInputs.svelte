<script lang="ts">
	let scoops: number = 1;
	let flavours: string[] = [];
	let testing: string[] = [];

	const formatter = new Intl.ListFormat('en', { style: 'long', type: 'conjunction' });
</script>

<div class="container">
	<div class="inside">
		<h2>Size</h2>

		{#each [1, 2, 3] as number}
			<label>
				<input type="radio" name="scoops" value={number} bind:group={scoops} />
				{number}
				{number === 1 ? 'scoop' : 'scoops'}
			</label>
		{/each}
	</div>
	<div class="inside">
		<h2>Flavours</h2>

		{#each ['cookies and cream', 'mint choc chip', 'raspberry ripple'] as flavour}
			<label>
				<input type="checkbox" name="flavours" value={flavour} bind:group={flavours} />
				{flavour}
			</label>
		{/each}

		{#if flavours.length === 0}
			<p>Please select at least on flavour</p>
		{:else if flavours.length > scoops}
			<p>Can't order more flavours than scoops</p>
		{:else}
			<p>
				You orderer {scoops}
				{scoops === 1 ? 'scoop' : 'scoops'} of {formatter.format(flavours)}
			</p>
		{/if}
	</div>
	<div class="inside">
		<h2>Using multiple selection</h2>

		<select multiple bind:value={testing}>
			{#each ['cookies and cream', 'mint choc chip', 'raspberry ripple'] as flavour}
				<option>
					{flavour}
				</option>
			{/each}
		</select>
	</div>
</div>

<style>
	.container {
		margin-top: 1rem;
		border: 1px solid black;
		width: 100%;
		padding: 0.5rem 1rem;
	}

	.inside {
		display: flex;
		flex-direction: column;

		& h2 {
			margin: 0.5rem 0;
			font-weight: bold;
		}
	}
</style>
