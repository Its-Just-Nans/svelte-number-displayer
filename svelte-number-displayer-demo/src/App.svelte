<script lang="ts">
    import * as easing from "svelte/easing";
    import { Displayer, DisplayerTweened } from "svelte-number-displayer";
    let num = 1000;
    let duration = 10;
    const getDefaultEasingNames = () => {
        const names = Object.keys(easing).filter((n) => !["default", "__moduleExports"].includes(n));
        return names.includes("linear") ? ["linear", ...names.filter((n) => n !== "linear")] : names;
    };
    const names = getDefaultEasingNames();
    let ease = (e) => e;
    let realoader = [];
</script>

<main>
    <h1>svelte-number-displayer-demo</h1>
    <a href="https://www.npmjs.com/package/svelte-number-displayer" target="_blank">
        <h3>npm - svelte-number-displayer</h3>
    </a>
    <a href="https://github.com/Its-Just-Nans/svelte-number-displayer" target="_blank">
        <h3>github - svelte-number-displayer</h3>
    </a>
    <div>
        <p>&lt;Displayer /&gt;</p>
        <p>(using requestAnimationFrame function)</p>
        {#key num && duration && realoader}
            <Displayer value={num} timing={duration} easing={ease} />
        {/key}
    </div>
    <br />
    <div>
        <p>&lt;DisplayerTweened /&gt;</p>
        <p>(using svelte tweened function)</p>
        {#key num && duration && realoader}
            <DisplayerTweened value={num} timing={duration} easing={ease} />
        {/key}
    </div>
    <hr />
    <p>End Number</p>
    <input bind:value={num} type="number" />
    <p>Duration</p>
    <input bind:value={duration} type="number" />
    <p>easing</p>
    <div>
        <select
            on:change={(e) => {
                ease = easing[e.target.value];
                realoader = [];
            }}
        >
            {#each names as name}
                <option value={name}>{name}</option>
            {/each}
        </select>
    </div>
</main>

<style>
</style>
