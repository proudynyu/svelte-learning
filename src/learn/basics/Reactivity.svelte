<script lang="ts">
	export let title: string = 'No title passed';
	let numbers = [1, 2, 3, 4, 5];

	function addNumber() {
		numbers = [...numbers, numbers.length + 1];
	}

    function removeLastNumber() {
        if (numbers.length > 1) {
            numbers = numbers.slice(0, numbers.length - 1) 
        }
    }

	$: sum = numbers.reduce((total, curr) => total + curr, 0);

	$: if (numbers.length > 10) {
		alert('Hold on a minute');
	}
</script>

{#if title}
	<h1>{title}</h1>
{/if}
<p>{numbers.join(' + ')} = {sum}</p>
<button on:click={addNumber}> add a number </button>
<button on:click={removeLastNumber}>remove last number </button>
