<script lang="ts">
	let promise = getRandomNumber();

	function handleClick() {
		promise = getRandomNumber();
	}

    async function sleep() {
        return new Promise((resolve) => {
            setTimeout(resolve, 2000)
        })
    }

	async function getRandomNumber() {
        await sleep()
		const res = await new Promise<number>((resolve) => {
			const number = Math.floor(Math.random() * 100);
			resolve(number);
		});

		return res;
	}
</script>

<div class="container">
    <button on:click={handleClick}> generate random number </button>
    
    {#await promise}
	<p>...waiting</p>
    {:then number}
	<p>The number is {number}</p>
    {:catch error}
	<p>An Error has occured {error.message}</p>
    {/await}
</div>

<style>
    .container {
        margin-top: 2rem;
    }
</style>