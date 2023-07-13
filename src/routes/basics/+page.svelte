<script>
    import ColorPicker from "../../learn/basics/ColorPicker.svelte";
import FirstComponent from "../../learn/basics/FirstComponent.svelte";
	import Package from "../../learn/basics/Package.svelte";
	import Reactivity from "../../learn/basics/Reactivity.svelte";

    const pkg = {
        name: "svelte",
        speed: "blazing",
        version: 4,
        website: "https://svelte.dev"
    }
</script>

<div>
    <FirstComponent />
    <Reactivity title="Reactivty with props"/>
    <Package {...pkg}/>
    <ColorPicker />
</div>

<style>
    div {
        flex: 1;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
</style>