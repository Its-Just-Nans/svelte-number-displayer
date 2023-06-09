# svelte-number-displayer

Display animated number easily with Svelte. Check the [demo](https://its-just-nans.github.io/svelte-number-displayer-demo) !

## Usage

```svelte
<script>
import Displayer from "svelte-number-displayer";
</script>

<Displayer value={20} timing={40} />
```

## Options

- `value`: the end value
- `timing`: the duration of the animation
- `defaultValue`: the start value (default `0`)
- `showTimer`: log the time of the animation
- `fnRound`: the rounding function
- `easing`: the easing function the change the linearity of the animation

## Other components

```svelte
<script>
import { DisplayerTweened } from "svelte-number-displayer";
import Displayer from "svelte-number-displayer";
</script>

<!-- it use the requestAnimationFrame function -->
<Displayer value={20} timing={40} />

<!-- it use the svelte tweened function -->
<DisplayerTweened value={20} timing={40} />
```

## License

Licensed under the MIT License - [LICENSE](LICENSE)
