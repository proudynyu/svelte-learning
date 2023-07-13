<script lang="ts">
    export let title: string = ""
    let numbers = [1, 2, 3, 4, 5]

    function addNumber() {
        numbers = [...numbers, numbers.length + 1]
    }

    $: sum = numbers.reduce((total, curr) => total + curr, 0)
</script>

{#if title}
    <h1>{title}</h1>
{/if}
<p>{numbers.join(" + ")} = {sum}</p>
<button on:click={addNumber}>
    add a number
</button>