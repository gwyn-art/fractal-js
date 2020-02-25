<script>
  import { onMount } from 'svelte';
  import { __DEV__ } from "./config";
  export let height;
  export let width;
  export let pallete;
  let canvas;
  let context;
  let id;

  $: (() => {
      if (!context) {
        return;
      }

      if (__DEV__) {
        console.time();
      }

      for (let index = 0; index < pallete.length; index++) {
        const colors = pallete[index];

        if (!Array.isArray(colors)) {
          return;
        }

        const [r, g, b] = colors;
        id.data[0 + index * 4] = r;
        id.data[1 + index * 4] = g;
        id.data[2 + index * 4] = b;
        id.data[3 + index * 4] = 255;
      }
      context.putImageData(id, 0, 0);
    if (__DEV__) console.timeEnd();
  })()

  onMount(() => {
    context = canvas.getContext("2d");
    context.fillRect(0, 0, width, height);
    id = context.getImageData(0, 0, width, height);
  });
</script>

<canvas {height} {width} bind:this={canvas} />
