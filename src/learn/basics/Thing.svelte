<script lang="ts">
    const emojis = {
		apple: '🍎',
		banana: '🍌',
		carrot: '🥕',
		doughnut: '🍩',
		egg: '🥚'
	};

    export let name: keyof typeof emojis;

    const emoji = emojis[name];
</script>

<p>{emoji} = {name}</p>