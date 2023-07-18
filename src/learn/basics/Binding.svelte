<script lang="ts">
	let name: string = 'Igor';
	let rangeA: number = 1;
	let rangeB: number = 2;

	let choose: boolean = false;

	let questions = [
		{
			id: 1,
			text: `Where did you go to school?`
		},
		{
			id: 2,
			text: `What is your mother's name?`
		},
		{
			id: 3,
			text: `What is another personal fact that an attacker could easily find with Google?`
		}
	];

	let selected: { id: number, text: string };
	let answer: string;
</script>

<div>
	<h1>Binding</h1>
	<input type="text" name="name" bind:value={name} />
	<p>Hello {name}</p>
	<br />

	<label>
		<input type="number" bind:value={rangeA} min="0" max="100" />
		<input type="range" bind:value={rangeA} min="0" max="100" />
	</label>
	<label>
		<input type="number" bind:value={rangeB} min="0" max="100" />
		<input type="range" bind:value={rangeB} min="0" max="100" />
	</label>

	<label>
		<input type="checkbox" name="check" bind:checked={choose} />
		Yes, send me the email!
	</label>

	{#if choose}
		<p>Great, we will send the email</p>
	{:else}
		<p>We will not send anything</p>
	{/if}

	<button disabled={!choose} on:click={() => alert('Sending')}>Subscribe</button>

	<form
		on:submit|preventDefault={() => alert(`
            Your question: ${selected.id}.${selected.text}\n
            Your response: ${answer}`
        )}
	>
		<select name="choices" id="" bind:value={selected}>
			{#each questions as question (question.id)}
				<option value={question}>{question.text}</option>
			{/each}
		</select>
		<input type="text" bind:value={answer} />
		<button type="submit" disabled={!answer}>Submit</button>
	</form>
</div>

<style>
	div {
		display: flex;
		flex-direction: column;
		margin-top: 2rem;
	}

	form {
		margin-top: 2rem;
	}
</style>
