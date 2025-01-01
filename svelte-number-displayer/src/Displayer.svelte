<script lang="ts">
    import { onMount } from "svelte";
    import { cubicOut } from "svelte/easing";
    export let value: number = 100;
    export let timing: number = 5;
    export let defaultValue: number = 0;
    export let showTimer: boolean = false;
    export let fnRound: (c: number) => number = Math.floor;
    export let easing: (c: number) => number = (n) => n;
    let valueDisplay = defaultValue;
    let currentTime = 0;
    const lerp = (x: number, y: number, t: number) => {
        return (1 - t) * x + t * y;
    };
    let lastTime: number;
    onMount(() => {
        let id = requestAnimationFrame(function display(delta) {
            const t = performance.now();
            const timer = (t - lastTime) / 1000;
            lastTime = t;
            currentTime = currentTime + timer;
            const currentValue = lerp(defaultValue, value, easing(currentTime / timing));
            valueDisplay = fnRound(currentValue);
            if (currentTime < timing) {
                id = requestAnimationFrame(display);
            } else {
                valueDisplay = value;
                if (showTimer) {
                    console.timeEnd("timer-number-displayer");
                }
            }
        });
        lastTime = performance.now();
        if (showTimer) {
            console.time("timer-number-displayer");
        }
        return () => cancelAnimationFrame(id);
    });
</script>

{valueDisplay}
