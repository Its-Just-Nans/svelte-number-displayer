<script lang="ts">
    import { onMount } from "svelte";
    import { tweened } from "svelte/motion";

    export let value: number = 100;
    export let timing: number = 5;
    export let fnRound: (c: number) => number = Math.floor;
    export let easing: (c: number) => number = (n) => n;
    const valueDisplay = tweened(0, {
        duration: timing * 1000,
        easing,
    });
    onMount(() => {
        valueDisplay.set(value);
    });
</script>

{fnRound($valueDisplay)}
